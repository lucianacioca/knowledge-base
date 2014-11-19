# OpenSSL #

## Generating self-signed certificate ##

RSA key :

~~~~~
openssl genrsa -out example.key 1024
~~~~~

Certificate Signing Request :

~~~~~
openssl req -new -key example.key -out example.csr
~~~~~

X509 certificate :

~~~~~
openssl x509 -req -days 365 -in example.csr -signkey example.key -out example.crt
~~~~~

## Removing passphrase on RSA key ##

~~~~~
openssl rsa -in my.key.with_passphrase -out my.key
~~~~~

