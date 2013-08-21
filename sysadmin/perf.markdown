
# Performances #

## URL ##

- http://dtrace.org/blogs/brendan/2012/03/07/the-use-method-linux-performance-checklist/

## Disk performance ##

Some average numbers :

~~~~~
Data access to RAM : 83 ns
Data access to hard drive : 13 ms
Average IOPS for a 10K RPM drive : 133
~~~~~

Sources : <http://blog.scoutapp.com/articles/2011/02/10/understanding-disk-i-o-when-should-you-be-worried>

### Ressources ###

- [Calculate IOPS in a storage array](http://www.techrepublic.com/blog/datacenter/calculate-iops-in-a-storage-array/2182)

## Web server load troubleshooting  ##

### General tools ###

- htop
- dstat
- vmstat

### Apache specific tools ###

- mod_status
- apachetop

### Client side ###

- Firebug (with Firefox)

### Disk and filesystem usage ###

- iotop
- iostat
- lsof

### Network ###

- tcpdump
- netstat

### Collect tools ###

- Munin
- collectd
- sysstat / sar

