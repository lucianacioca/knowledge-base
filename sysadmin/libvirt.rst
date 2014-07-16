Libvirt
=======

List networks : ::

    virsh -c qemu:///system net-list

Show ``default`` network config : ::

    virsh -c qemu:///system net-dumpxml default

List storages : ::

    virsh -c qemu:///system pool-list

Show ``default`` storage config : ::

    virsh -c qemu:///system pool-dumpxml default

Change default images store location (then edit ``<path>``) : ::

    virsh pool-edit default

