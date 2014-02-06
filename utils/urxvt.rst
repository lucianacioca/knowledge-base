
=====
urxvt
=====

urxvt is a great terminal emulator which can be extended using Perl.

Perl extensions
===============
The man page urxvtperl(3) documents Perl extensions coding.

To enable debugging, define this environment variable : ::

    # == 0 - fatal messages
    # >= 3 - script loading and management
    # >=10 - all called hooks
    # >=11 - hook return values
    export URXVT_PERL_VERBOSITY=3

