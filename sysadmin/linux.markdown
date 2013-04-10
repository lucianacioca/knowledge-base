# Linux #

Up-to-date list of kernel parameters : <https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/kernel-parameters.txt>

## Kernel logging rate limiting ##

Minimal number of seconds between messageS :

~~~~~
cat /proc/sys/kernel/printk_ratelimit
~~~~~

Number of messages by *printk_ratelimit* seconds :

~~~~~
cat /proc/sys/kernel/printk_ratelimit_burst
~~~~~

