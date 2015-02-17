
Debian installation
===================

This file documents the low-level installation tasks I perform manually on a fresh bare-metal server.
All remaining actions are performed by Salt.

These instructions are valid for Debian 7 *Wheezy*.

Note : 192.0.2.0/24, 198.51.100.0/24 and 203.0.113.0/24 are example networks described in RFC 5737.

Naming
------

- Set short hostname in ``/etc/hostname`` (eg. ``host1``)
- Set full hostname in ``/etc/mailname`` (eg. ``host1.example.com``)

Edit ``/etc/hosts`` according to this example : ::

    127.0.0.1 localhost
    127.0.1.1 host1.example.com host1

At this point, the ``hostname -f`` should return the full hostname without latency.

Networking
----------

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

Example for adding additional IP addresses : ::

    auto eth0:1
    iface eth0:1 inet static
        address 203.0.113.1
        broadcast 203.0.113.1
        netmask 255.255.255.0

Example for bridging (also need to install ``bridge-utils``) : ::

    auto br0
    iface br0 inet static
        bridge_ports eth1
        bridge_stp off
        bridge_fd 0
        bridge_maxwait 0

Firewall
--------
TODO

DNS resolution
--------------
If installed, remove bind : ::

    apt-get purge bind9 bind9utils

Install unbound : ::

    apt-get install unbound

Edit ``/etc/resolv.conf`` according to this example : ::

    nameserver 127.0.0.1
    search example.com

Security
--------

**[OVH_ specific]** Move SSH keys from ``/root/.ssh/authorized_keys2`` (if present) to
``/root/.ssh/authorized_keys``, and comment OVH keys.

If not already done, set a strong or disabled password for the root account.

Packages
--------
Configure ``/etc/apt/sources.list``. Example : ::

    deb http://ftp.fr.debian.org/debian/ wheezy main
    deb http://security.debian.org/ wheezy/updates main
    [...]

Then execute : ::

    apt-get update
    apt-get dist-upgrade

Remove package ``mlocate`` which can be responsible for huge I/O : ::

    apt-get purge mlocate

**[OVH specific]** Remove RAID utilities responsible for check_raid problems (unless needed) : ::

    mv /sbin/MegaCli /sbin/tw_cli /sbin/mpt-status /tmp/

Kernel
------

Check the installed and running kernel.

If LXC will be used, enable cgroup filesystem : ::

    echo "cgroup  /sys/fs/cgroup  cgroup  defaults  0   0" >>/etc/fstab
    mount /sys/fs/cgroup

Volume management
-----------------

Create a large LVM volume group.

**[OVH specific]** Unmount ``/home``, remove it from ``/etc/fstab``, ``pvcreate
/dev/mdX``, ``vgcreate vg1 /dev/mdX``.

Salt
----

Add to sources.list : ::

    deb http://debian.saltstack.com/debian wheezy-saltstack main

Execute : ::

    apt-get install ca-certificates
    wget -q -O- "https://debian.oopss.org/keys/debian-salt-team-joehealy.gpg.key" | apt-key add -
    apt-get update
    apt-get dist-upgrade
    apt-get install salt-minion

Add ``salt`` entry to ``/etc/hosts``, then : ::

    service salt-minion restart

Reboot
------

Finally, perform a final reboot.

Before going to production, check my `QA page`_.

.. _QA page: https://github.com/tmartinfr/knowledge-base/blob/master/sysadmin/qa.rst
.. _OVH: http://www.ovh.com/

