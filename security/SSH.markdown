
# SSH Security #

These rules works for Debian systems with the default SSHD configuration.



1. Forbid root login (`PermitRootLogin No`), or allow only public key (`PermitRootLogin without-password`)

2. Forbid password authentification (`PasswordAuthentication no`)

3. If necessary to use password authentification from particular places (e.g. admin workstations), allow only these IP addresses/networks :

 ~~~~~
 PasswordAuthentication No
 Match Address 192.0.2.1,192.0.2.2,192.0.1.0/24
     PasswordAuthentication yes
 ~~~~~

4. If some users need password authentification from everywhere, allow only these users and check password robustness :

 ~~~~~
 Match User bob, fred
     PasswordAuthentication yes
 ~~~~~

5. Restrict SSH access to the group `sshusers` :

 ~~~~~
 AllowGroups sshusers
 ~~~~~

6. Set a very complicated and random root password and store it securely (will not be used)

7. If possible, restrict network access to the SSH port or use a non-standard port number

