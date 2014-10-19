
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

Troubleshooting
---------------

If the following error appears when executing the ``reclass`` binary : ::

    Traceback (most recent call last):
      File "/usr/bin/reclass", line 5, in <module>
        from pkg_resources import load_entry_point
    ImportError: No module named pkg_resources

then install the ``python-pkg-resources`` package (on Debian).

