# Debian #

## Packaging ##

### Example package

Get source :

~~~~~
apt-get source hello-debhelper
~~~~~

Following files are extracted in current directory :

~~~~~
hello-debhelper-2.6                    # Full source tree
hello-debhelper_2.6-2.debian.tar.gz    # Debian specific files (debian/ dir)
hello-debhelper_2.6-2.dsc              # Package description, PGP signed
hello-debhelper_2.6.orig.tar.gz        # Original tarball
~~~~~

Simple package build :

~~~~~
cd hello-debhelper-2.6
./debian/rules build
fakeroot ./debian/rules binary
~~~~~

