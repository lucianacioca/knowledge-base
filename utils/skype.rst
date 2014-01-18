
=====
Skype
=====

Skype is non-free software but I often need it.

Good news, it runs well on Debian Wheezy amd64.

Installation
============

Enable multi-arch : ::

    dpkg --add-architecture i386

Download package from the `skype-for-linux <http://www.skype.com/fr/download-skype/skype-for-linux/>`_ page, then install it : ::

    dpkg -i skype-debian_4.2.0.11-1_i386.deb

Install i386 dependencies : ::

    apt-get -f install
    apt-get install libpulse0:i386

