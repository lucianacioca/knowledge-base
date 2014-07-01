
reclass
=======

Backport for Wheezy
-------------------

Ensure the following line is present in ``/etc/apt/sources.list`` : ::

    deb-src http://ftp.fr.debian.org/debian/ jessie main

Then fetch the source package : ::

    apt-get source reclass

And install build dependencies : ::

    apt-get build-dep reclass

Build package : ::

    debuild -uc -us

