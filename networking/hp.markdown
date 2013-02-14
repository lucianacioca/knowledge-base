# HP #

## CLI ##

Create VLAN 99 with name VLAN_A :

~~~~~
vlan 99 name VLAN_A
~~~~~

Remove VLAN 99 :

~~~~~
no vlan 99
~~~~~

Add tagged VLAN 99 on interface 2 :

~~~~~
vlan 99 tag 2
~~~~~

Remove tagged VLAN 99 on interface 2 :

~~~~~
vlan 99 untag 2
~~~~~

Add untagged VLAN 99 on interface 2 :

~~~~~
vlan 99 untagged 2
~~~~~

Save memory :

~~~~~
wr mem
~~~~~

