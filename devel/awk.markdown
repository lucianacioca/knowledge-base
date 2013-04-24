# Awk #

Following examples uses `mawk` from Debian 6.0.

## Examples ##

Regex and parenthesis captures :

~~~~~
awk 'match($0, /(My_Pattern)/, m) {print m[1]}'
~~~~~

