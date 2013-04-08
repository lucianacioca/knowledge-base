# KVM #

## Basic usage ##

Debian installation :

~~~~~
qemu-img create -f qcow2 /mnt/kvm/example.qcow2 20G
kvm -hda /mnt/kvm/example.qcow2 -cdrom /mnt/share/comp/debian-6.0.7-a-CD-1.iso -boot d -m 1024 -k fr
~~~~~

