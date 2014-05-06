
===
LXC
===

Web ressources
==============

- `Official homepage <http://lxc.sourceforge.net/>`_

- `LXC page on Debian wiki <http://wiki.debian.org/LXC/>`_

- `LXC 1.0: Blog post series <https://www.stgraber.org/2013/12/20/lxc-1-0-blog-post-series/>`_

Command line
============

Create container with template ``ubuntu`` and name ``container1`` : ::

    lxc-start -t ubuntu -n container1

List available templates : ::

    ls /usr/share/lxc/templates/

Show available options for template : ::

    /usr/share/lxc/templates/lxc-debian -h

Start container in background : ::

    lxc-start -n container1 -d

Execute bash directly in the container : ::

    lxc-attach -n container1

Get info about the container : ::

    lxc-info -n container1

Stop container : ::

    lxc-stop -n container1

Kill container : ::

    lxc-kill -n container1

Freeze container : ::

    lxc-freeze -n container1

List configuration file directives : ::

    man 5 lxc.conf

