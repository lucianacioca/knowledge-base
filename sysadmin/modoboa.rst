
Modoboa setup (DRAFT)
=====================

This setup installs and configures Modoboa with LDAP authentication.

Modoboa
-------

Install requirements and software ::

    apt-get install python-pip python-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev
    apt-get install postgresql
    pip install modoboa python-ldap django-auth-ldap

Create database ::

    sudo -u postgres psql;
    create user modoboa with password 'xxx';
    create database modoboa with owner modoboa encoding 'UTF-8';

Deploy ::

    modoboa-admin.py deploy <modoboa_site> --dbaction install --collectstatic \
        --dburl postgres://modoboa:xxx@127.0.0.1/modoboa \
        --domain <domain on which Modoboa's web interface is acceded>
    cd modoboa
    # Setting DEBUG = True is required to use modoboa with Django's web server
    python manage.py runserver 0.0.0.0:8000

Add ``'modoboa.lib.authbackends.LDAPBackend`` as first entry to the
``AUTHENTICATION_BACKENDS`` setting in ``settings.py``.

Dovecot
-------

Install requirements and software  ::

    apt-get install dovecot-imapd dovecot-pop3d postfix dovecot-pgsql dovecot-lmtpd

Dovecot parameters in ``conf.d/10-mail.conf`` ::

    mail_location = maildir:~/.maildir

    namespace inbox {
    [...]
        mailbox Drafts {
          auto = subscribe
          special_use = \Drafts
        }
        mailbox Junk {
          auto = subscribe
          special_use = \Junk
        }
        mailbox Sent {
          auto = subscribe
          special_use = \Sent
        }
        mailbox Trash {
          auto = subscribe
          special_use = \Trash
        }
    }

Add this crontab on the modoboa account : ::

    * * * * * python <modoboa_site>/manage.py handle_mailbox_operations

Let only the ``!include auth-sql.conf.ext`` include at the end of ``conf.d/10-auth.conf``.

Edit ``dovecot-sql.conf.ext`` and set ::

    driver = pgsql
    connect = host=127.0.0.1 dbname=modoboa user=modoboa password=xxx
    default_pass_scheme = CRYPT
    password_query = SELECT email AS user, password FROM core_user WHERE email='%u' and is_active
    user_query = SELECT '<mailboxes storage directory>/%d/%n' AS home, <uid> as uid, <gid> as gid, '*:bytes=' || mb.quota || 'M' AS quota_rule FROM admin_mailbox mb INNER JOIN admin_domain dom ON mb.domain_id=dom.id WHERE mb.address='%n' AND dom.name='%d'
    iterate_query = SELECT email AS username FROM core_user WHERE email<>''

Edit ``conf.d/10-master.conf`` and set : ::

    service lmtp {
      unix_listener /var/spool/postfix/private/dovecot-lmtp {
        mode = 0600
        user = postfix
        group = postfix
    }

Test : ::

    mutt -f imap://thomas@modoboa1.local:xxx@localhost:143

Postfix
-------

Install requirements and software ::

    apt-get install postfix postfix-pgsql

Generate Postfix maps : ::

    modoboa-admin.py postfix_maps --dbtype postgres /etc/postfix/maps

Add config to main.cf : ::

    virtual_transport = lmtp:unix:private/dovecot-lmtp
    relay_domains =
    virtual_mailbox_domains = pgsql:/etc/postfix/maps/sql-domains.cf
    virtual_alias_domains = pgsql:/etc/postfix/maps/sql-domain-aliases.cf
    virtual_alias_maps = pgsql:/etc/postfix/maps/sql-aliases.cf,
          pgsql:/etc/postfix/maps/sql-domain-aliases-mailboxes.cf,
          pgsql:/etc/postfix/maps/sql-mailboxes-self-aliases.cf,
          pgsql:/etc/postfix/maps/sql-catchall-aliases.cf
    smtpd_recipient_restrictions =
          check_recipient_access pgsql:/etc/postfix/maps/sql-maintain.cf
          permit_mynetworks
          reject_unverified_recipient

