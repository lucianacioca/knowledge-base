
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

### Benchmark with bonnie++ ###

~~~~~
# Perform benchmark as user nobody (-u) into directory /tmp (-d), using a file
# twice as big as the total RAM (-s), without write buffering (-b).
# Skip per-char IO tests (-f).
# Save results in file bonnie.timestamp.

bonnie++ -u nobody -d /tmp \
    -s $(perl -ne '/^MemTotal:\s+(\d+)/ && print int($1/512+1)' /proc/meminfo) \
    -b -f >/root/bonnie.$(date +%s)
~~~~~

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
- bonnie++

### Network ###

- tcpdump
- netstat

### Collect tools ###

- Munin
- collectd
- sysstat / sar

