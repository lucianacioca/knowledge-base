
==============================
Server post-install guidelines
==============================

This page aims to summarize all particular points to take into account when
configuring an UNIX-type server.

All servers MUST have
---------------------

- **Naming, networking and DNS** correctly defined (see below)
- **NTP** server synchronized on pool.ntp.org
- **Backup** of sensitive data with incremental archives
- **Dump** of each databases, each day
- **Metrics** of all system components
- **Firewall** enabled with restrictive ruleset
- **Root password** disabled or very complex
- **Packages repository** correctly configured, with security updates
- **Root e-mail alias** directed to a human sysadmin mailbox
- **SSH access** secured (see below)
- **Monitoring** of all services and subsystems, including :
    - Security updates
    - Storage and RAID status

All servers SHOULD have
-----------------------

- **Configuration management** allowing to reinstall the server from scratch
- **Documentation** of system operations
- **Kernel** up-to-date and minimized for the server task

Prefered tools on Debian
------------------------

========================   ===================================
Task                       Software
========================   ===================================
NTP                        NTPD
Backup                     tobackup
Metrics                    Munin
Firewall                   Iptables/Netfilter
Monitoring                 Nagios
Configuration management   SaltStack
Documentation              Sphinx
========================   ===================================

Naming, networking and DNS
--------------------------

Note : this is my way of doing things and it tries to respect Debian policies.
It's only tested on Debian 7 *Wheezy*. 

Naming
^^^^^^

- Set short hostname in ``/etc/hostname`` (eg. ``host1``)
- Set full hostname in ``/etc/mailname`` (eg. ``host1.example.com``)

Edit ``/etc/hosts`` according to this example : ::

    127.0.0.1 localhost
    127.0.1.1 host1.example.com host1

At this point, the ``hostname -f`` should return the full hostname without latency.

Basic IPv4 networking
^^^^^^^^^^^^^^^^^^^^^

Edit ``/etc/network/interfaces`` according to this example : ::

    # This file describes the network interfaces available on your system
    # and how to activate them. For more information, see interfaces(5).

    # The loopback network interface
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
        address 192.0.2.1
        netmask 255.255.255.0
        gateway 192.0.2.254

DNS resolution
^^^^^^^^^^^^^^

If installed, remove bind : ::

    apt-get purge bind9 bind9utils

Install unbound : ::

    apt-get install unbound

Edit ``/etc/resolv.conf`` according to this example : ::

    nameserver 127.0.0.1
    search example.com

SSH Security
------------

These rules work for Debian systems with default SSHD configuration.

1. Restrict root login (``PermitRootLogin No``), or allow only public key (``PermitRootLogin without-password``)

2. Restrict password authentification (``PasswordAuthentication no``)

3. If necessary to use password authentication from particular places (e.g. admin workstations), allow only these IP addresses/networks : ::

    PasswordAuthentication No
    Match Address 192.0.2.1, 192.0.2.2, 192.0.1.0/24
        PasswordAuthentication yes

4. If some users need password authentication from everywhere, allow only these users and check their passwords robustness : ::

    Match User bob, fred
        PasswordAuthentication yes

5. Restrict SSH access to the group ``sshusers`` : ::

    AllowGroups sshusers

8. Install sudo, and add authorized users to the sudo group

7. If possible, restrict network access to the SSH port or use a non-standard port number

