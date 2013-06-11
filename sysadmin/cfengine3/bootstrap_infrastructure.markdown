
# Procédures #

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

- domain
- acl

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

