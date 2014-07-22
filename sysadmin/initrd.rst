
=================
Initrd management
=================

Debian
======
Edit initrd files in ``/usr/share/initramfs-tools/``.

Then, rebuild using : ::

    update-initramfs -ut

To obtain debugging informations, boot with the ``debug`` kernel parameter,
then check the content of ``/run/initramfs/``.

More informations in :

- https://wiki.debian.org/initramfs
- https://wiki.debian.org/InitramfsDebug

