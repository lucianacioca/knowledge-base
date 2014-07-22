
Debian installation
===================

This documentation is currently valid for Debian 6.0 and 7.0.

Note : 192.0.2.0/24, 198.51.100.0/24 and 203.0.113.0/24 are example networks described in RFC 5737.

Partitioning and RAID
---------------------

Partitioning and RAID configuration should be performed according to the server usage.

Example 1 : RAID 5 over 7 disks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This configuration is performed on a OVH server installed with standard partitioning layout : ::

    apt-get install gdisk

    # Stop RAID on /home device
    umount /home
    mdadm --stop /dev/md3

    for drive in sda sdb sdc sdd sde sdf sdg; do
            device="/dev/$drive"

            # Disable swap
            swapoff ${device}3

            # Remove home and swap partitions when existing
            sgdisk --delete=3 $device
            sgdisk --delete=4 $device

            # Create partitions for RAID and swap
            sgdisk --new=3:40962048:42008575 $device
            sgdisk --new=4:42008576:-1 $device
            sgdisk --typecode=3:8200 $device   # type = swap
            sgdisk --typecode=4:fd00 $device   # type = linux-raid

            # Recreate swap partition
            mkswap ${device}3
    done

    # Create RAID5 array
    mdadm --create /dev/md3 --level=5 --raid-devices=7 /dev/sda4 /dev/sdb4 /dev/sdc4 /dev/sdd4 /dev/sde4 /dev/sdf4 /dev/sdg4

    # Create volume group
    vgcreate vg1 /dev/md3

    # Check and mount the correct devices
    vim /etc/fstab

Result : ::

    root@haz7:~# gdisk -l /dev/sda
    GPT fdisk (gdisk) version 0.8.5

    Partition table scan:
      MBR: protective
      BSD: not present
      APM: not present
      GPT: present

    Found valid GPT with protective MBR; using GPT.
    Disk /dev/sda: 7814037168 sectors, 3.6 TiB
    Logical sector size: 512 bytes
    Disk identifier (GUID): F52A1D83-550E-4881-B305-B614A09BBA71
    Partition table holds up to 128 entries
    First usable sector is 34, last usable sector is 7814037135
    Partitions will be aligned on 8-sector boundaries
    Total free space is 2054 sectors (1.0 MiB)

    Number  Start (sector)    End (sector)  Size       Code  Name
       1              40            2048   1004.5 KiB  EF02  primary
       2            4096        40962047   19.5 GiB    FD00  primary
       3        40962048        42008575   511.0 MiB   8200
       4        42008576      7814037134   3.6 TiB     FD00

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
``/root/.ssh/authorized_keys2`` (if present) to ``/root/.ssh/authorized_keys``,
and comment OVH keys.

If not already done, set a strong or disabled password for the root account.

.. _OVH: http://www.ovh.com

Packages update
---------------
Configure ``/etc/apt/sources.list``. Example for a Oopss_ server : ::

    deb http://debian.mirrors.ovh.net/debian/ wheezy main
    deb http://security.debian.org/ wheezy/updates main
    deb http://dist.oopss.org/debian/ wheezy/oopss main

Then execute : ::

    apt-get update
    apt-get upgrade

.. _Oopss: http://oopss.org

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

