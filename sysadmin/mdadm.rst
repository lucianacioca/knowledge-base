mdadm
=====

Query
-----

Print mdstat summary : ::

    cat /proc/mdstat

Show details of a particular MD device : ::

    mdadm --query --detail /dev/md1

Disk failure
------------

Example case :

- Array ``/dev/md1`` contains ``/dev/sda`` and ``/dev/sdb``
- ``/dev/sda`` has failed

How-to :

- Replace disk ``/dev/sda``

- Copy partition table : ::

    sfdisk -d /dev/sdb | sfdisk --force /dev/sda

- Add missing device for each partition : ::

    mdadm /dev/md1 --manage --add /dev/sda1
    [...]

- Check the repair state with ``/proc/mdstat``

