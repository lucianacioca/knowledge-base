# Multitail #

## Example usage ##

Note : the following examples often need a special configuration in `/etc/multitail.conf`. Normally, your multitail package should provide it.

Open Nagios log file and convert timestamps to human-readable dates :

~~~~~
multitail -cv nagios.log nagios.log
~~~~~
