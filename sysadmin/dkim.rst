
========
OpenDKIM
========

Deployment on Debian Squeeze with Postfix
=========================================

*Warning : this howto is work in progress*

Ressources :

- `RFC 4871 - The DKIM-Signature Header Field <http://tools.ietf.org/html/rfc4871#section-3.5>`_
- `RFC 4871 - Key Management and Representation <http://tools.ietf.org/html/rfc4871#section-3.6>`_

Install package : ::

    aptitude install opendkim

Generate keys pair : ::

    cd /etc/ssl
    openssl genrsa -out example.com.dkim.private.key 1024
    openssl rsa -in example.com.dkim.private.key \
       -pubout -out example.com.dkim.public.key
    chown opendkim example.com.dkim.private.key

Add OpenDKIM configuration for desired domain : ::

    cat <<EOT >>/etc/opendkim.conf
    Domain   example.com
    KeyFile  /etc/ssl/example.com.dkim.private.key
    Selector 2013
    EOT

Enable network socket : ::

    cat <<EOT >>/etc/default/opendkim
    SOCKET="inet:8891:localhost"
    EOT

Note we can't use the default unix socket (``/var/run/opendkim/opendkim.sock``) because Postfix is chrooted. Another way could be to change this path to put the socket in ``/var/spool/postfix``.

Start OpenDKIM : ::

    /etc/init.d/opendkim start

Add following Postfix configuration in ``/etc/postfix/main.cf`` : ::

    # DKIM
    milter_default_action = accept
    milter_protocol = 6
    smtpd_milters = inet:127.0.0.1:8891
    non_smtpd_milters = inet:127.0.0.1:8891

Restart Postfix, send test e-mail, and check logs : ::

    /etc/init.d/postfix restart
    date | /usr/sbin/sendmail  -f exp@example.com dest@example.com
    tail -f /var/log/mail.log

The received e-mail should have a ``DKIM-Signature:`` header.

