Debian packaging
================

Useful packages
---------------

================ ==============================================================
Package          Description
================ ==============================================================
build-essential  Informational list of build-essential packages
debhelper        Helper programs for debian/rules
devscripts       Scripts to make the life of a Debian Package maintainer easier
dpkg-dev         Debian package development tools
dh               Debhelper command sequencer
dh-make          Tool that converts source archives into Debian package source
fakeroot         Tool for simulating superuser privileges
lintian          Debian package checker
quilt            Tool to work with series of patches
================ ==============================================================

Useful commands
---------------

================ ==============================================================
Command          Description
================ ==============================================================
dpkg-source      Packs and unpacks Debian source archives
dh_make          Prepare Debian packaging for an original source archive
================ ==============================================================

Useful URL
----------

================ ==============================================================
Link             Description
================ ==============================================================
WNPP_            Debian Packages that Need Lovin'
intro-maint_     Introduction for maintainers on mentors.debian.net
packaging-tuto_  Debian packaging tutorial
maint-guide_     Debian New Maintainers' Guide
tools_           1.2. Programs needed for development
help_            1.4. Where to ask for help
devel-reference_ Debian Developer's Reference
policy_          Debian Policy Manual
debian_ml_       Full list of Debian mailing lists
debian_ment_faq_ Debian Mentors FAQ
================ ==============================================================

.. _WNPP: http://wnpp.debian.net/
.. _intro-maint: http://mentors.debian.net/intro-maintainers
.. _packaging-tuto: http://www.debian.org/doc/manuals/packaging-tutorial/packaging-tutorial.en.pdf
.. _maint-guide: http://www.debian.org/doc/manuals/maint-guide/
.. _tools: http://www.debian.org/doc/manuals/maint-guide/start.en.html#needprogs
.. _help: http://www.debian.org/doc/manuals/maint-guide/start.en.html#helpme
.. _devel-reference: http://www.debian.org/doc/manuals/developers-reference/index.html
.. _policy: http://www.debian.org/doc/debian-policy/
.. _debian_ml: http://www.debian.org/MailingLists/subscribe
.. _debian_ment_faq: https://wiki.debian.org/DebianMentorsFaq

Useful mailing lists (personal interest)
----------------------------------------

- debian-mentors
- debian-announce
- debian-enterprise
- debian-devel-announce
- debian-news
- debian-devel
- debian-project
- debian-releases
- debian-qa
- debian-security
- debian-security-announce
- debian-stable-announce
- debian-cloud

How-to build an existing package
--------------------------------

Get source and install build dependencies : ::

    apt-get build-dep hello-debhelper
    apt-get source hello-debhelper

Following files are extracted in current directory : ::

    hello-debhelper-2.6                    # Full source tree
    hello-debhelper_2.6-2.debian.tar.gz    # Debian specific files (debian/ dir)
    hello-debhelper_2.6-2.dsc              # Package description, PGP signed
    hello-debhelper_2.6.orig.tar.gz        # Original tarball

Alternative 1 : Manual build
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Directly run the main building script (``debian/rules``) : ::

    cd hello-debhelper-2.6
    ./debian/rules build
    fakeroot ./debian/rules binary

Alternative 2 : Use debhelper
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Run ``debhelper`` using ``-uc -us`` to disable signing the package : ::

    cd hello-debhelper-2.6
    debuild -uc -us

How-to create source package for a simple script
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I often write simple sysadmin scripts, consisting of a single architecture
independent shell script.

Here is a simple way to package it.

Create base directory with a version number : ::

    mkdir lxc-debootstrap-1.0
    cd lxc-debootstrap-1.0

Put the script into the directory : ::

    cp /some/path/lxc-debootstrap .

Execute ``dh_make`` and confirm : ::

    # --createorig allows to not supply orig tarball, and to let ``dh_make`` generate it
    # -i sets the package class to arch-independent
    dh_make --createorig -i

