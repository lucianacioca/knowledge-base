
Debian post-install
===================

This documentation is currently valid for Debian 6.0 and 7.0.

Note : 192.0.2.0/24, 198.51.100.0/24 and 203.0.113.0/24 are example networks described in RFC 5737.

Naming
------

- Set short hostname in ``/etc/hostname`` (eg. ``host1``)
- Set full hostname in ``/etc/mailname`` (eg. ``host1.example.com``)

Edit ``/etc/hosts`` as this : ::

    127.0.0.1 localhost
    127.0.1.1 host1.example.com host1

Networking
----------

Adjust ``/etc/network/interfaces`` as the following example : ::

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

If additional IP addresses are needed, add : ::

    auto eth0:1
    iface eth0:1 inet static
        address 203.0.113.1
        broadcast 203.0.113.1
        netmask 255.255.255.0

Bridging
^^^^^^^^

If internal bridging is needed (e.g. for LXC or KVM), add : ::

    auto br0
    iface br0 inet static
        bridge_ports none
        address 198.51.100.254
        netmask 255.255.255.0
        bridge_stp off
        bridge_fd 0
        bridge_maxwait 0

And execute : ::

    apt-get install bridge-utils

Security
--------

If using servers provided by OVH_, move keys from
``/root/.ssh/authorized_keys2`` to ``/root/.ssh/authorized_keys``, and comment
OVH keys.

If not already done, set a strong or disabled password for the root account.

.. _OVH: http://www.ovh.com

Packages update
---------------

Check sources.list, then execute : ::

    apt-get update
    apt-get upgrade

Kernel
------

If the server runs an OVH kernel, install a Debian default kernel and disable OVH kernel : ::

    apt-get install linux-image-amd64
    mv /etc/grub.d/06_OVHkernel /etc/grub.d/99_OVHkernel
    update-grub

If LXC will be used, enable cgroup filesystem : ::

    echo "cgroup  /sys/fs/cgroup  cgroup  defaults  0   0" >>/etc/fstab
    mount /sys/fs/cgroup

Reboot
------

Finally, perform a final reboot.

Before going to production, check my `QA page`_.

.. _QA page: https://github.com/tmartinfr/knowledge-base/blob/master/sysadmin/qa.rst
.. _OVH: http://www.ovh.com/

