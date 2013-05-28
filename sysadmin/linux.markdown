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

## Enable core dumps system-wide ##

Validated on RHEL 5.
Can be useful on development systems.

~~~~~
sysctl -w fs.suid_dumpable=2

mkdir -p -m 777 /var/local/dumps
echo "/var/local/dumps/core.%e.%p"> /proc/sys/kernel/core_pattern

cat <<EOT >>/etc/security/limits.conf
root hard core unlimited
root soft core unlimited
EOT
~~~~~

Then, ensure the programs you want to get a core do not lower their soft limits :

- `/etc/profile` for shell sessions
- Init scripts for daemons

Finally, reboot.

