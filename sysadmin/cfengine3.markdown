
# CFEngine 3 #

_CFEngine is an IT infrastructure automation framework that helps engineers, system administrators and other stakeholders in an IT system to manage and understand IT infrastructure throughout its lifecycle. CFEngine takes systems from Build to Deploy, Manage and Audit. [<http://cfengine.com/what-is-cfengine>]_

## URL ##

[CFEngine Downloads](http://cfengine.com/downloads)

[Latest Debian Packages](http://cfengine.com/pub/apt/pool/main/c/cfengine-community/)

[CFEngine reference manual](http://cfengine.com/manuals/cf3-reference)

## cf-sketch ##

[Installing cf-sketch](https://github.com/cfengine/design-center/wiki/Installing-cfsketch)

cf-sketch is written in Perl.

Currently there is no Debian packages available.

### Manual installation ###

Install some dependencies :

```
aptitude install libcrypt-ssleay-perl libterm-readline-gnu-perl
```

Get last version from GitHub :

```
wget --no-check-certificate https://github.com/downloads/cfengine/design-center/cf-sketch-latest.tar.gz
tar xf cf-sketch-latest.tar.gz
```

Use make to install in `/usr/local/bin` by default :

```
cd cf-sketch
make install
```

## Logging ##

See <http://cfengine.com/manuals/cf3-Reference#Text-logs>.

`cf-serverd` logs incoming requests using **syslog**.

`/var/cfengine/cf3.HOSTNAME.runlog` is the main logfile for looking at CFEngine activity.

`/var/cfengine/cfagent.HOSTNAME.log` could be deleted (obsolete).

`/var/cfengine/promise_summary.log` is useful to check that all promises are kept.
It could be monitored by a Nagios plugin.

## Bootstrap new infrastructure ##

### CFEngine server

Download CFEngine package in `/root/install/` (current used version : 3.4.4).

Install package manually, using `apt-get`.

Initialize GIT repository :

~~~~~
cd /var/cfengine/masterfiles/
git init
echo cf_promises_validated >.gitignore
git add .
git commit -m "Initial CFEngine files"
~~~~~

Clean-up unused files :

~~~~~
git rm cf-sketch-runfile.cf services/init_msg.cf
rmdir services/
git commit -m "Remove unused files"
~~~~~

Edit `def.cf` and set the following variables :

- `domain`
- `acl` (do not forget 127.0.0.1 !)

Edit `update.cf` and set `leaf_name => { ".*" };` for `body file_select u_input_files`.

Edit `controls/cf_serverd.cf` and add `-K` option to `cfruncommand`.

Edit `controls/cf_agent.cf` and add :

~~~~~
default_repository => "$(sys.workdir)/backup";
~~~~~

Edit `promises.cf` and :

- Remove `cfsketch_run` from `bundlesequence`
- Remove `cf-sketch-runfile.cf` and `services/init_msg.cf` from `inputs`
- Remove `INIT MSG` from `bundle agent main`

Commit :

~~~~~
git commit -a -m "Initial CFEngine configuration"
~~~~~

Add oopss-cf library :

~~~~~
git submodule add git@github.com:oopss/oopss-cf.git libraries/oopss-cf
git submodule init
git commit -m "Add oopss-cf library"
~~~~~

Define CFEngine server IP address (use external IP address or internal bridge address, but not the loopback address), then bootstrap :

~~~~~
IPADDR=192.0.2.1
/var/cfengine/bin/cf-agent -B -s $IPADDR
~~~~~

Finally, begin to code the infrastructure by adding method calls in bundle `main`.
