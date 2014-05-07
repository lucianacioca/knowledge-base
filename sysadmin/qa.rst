
=================
Quality assurance
=================

All servers MUST have
---------------------

- **NTP** server synchronized on pool.ntp.org
- **Backup** of sensitive data with incremental archives
- **Dump** of each databases, each day
- **Metrics** of all system components
- **Firewall** enabled with restrictive ruleset
- **Root password** disabled or very complex
- **Packages repository** correctly configured, with security updates
- **Root e-mail alias** directed to a human sysadmin mailbox
- **SSH access** secured (see section below)
- **Monitoring** of all services and subsystems, including :
    - Security updates
    - Storage and RAID status

All servers SHOULD have
-----------------------

- **Configuration management** allowing to reinstall the server from scratch
- **Documentation** of system operations

Prefered tools on Debian
------------------------

========================   ===================================

========================   ===================================
NTP                        OpenNTPD
Backup                     tobackup
Metrics                    Munin
Firewall                   Iptables/Netfilter
Monitoring                 Nagios
Configuration management   SaltStack
Documentation              Sphinx
========================   ===================================

SSH Security
------------

These rules work for Debian systems with default SSHD configuration.

1. Restrict root login (``PermitRootLogin No``), or allow only public key (``PermitRootLogin without-password``)

2. Restrict password authentification (``PasswordAuthentication no``)

3. If necessary to use password authentication from particular places (e.g. admin workstations), allow only these IP addresses/networks : ::

    PasswordAuthentication No
    Match Address 192.0.2.1, 192.0.2.2, 192.0.1.0/24
        PasswordAuthentication yes

4. If some users need password authentication from everywhere, allow only these users and check their passwords robustness : ::

    Match User bob, fred
        PasswordAuthentication yes

5. Restrict SSH access to the group ``sshusers`` : ::

    AllowGroups sshusers

8. Install sudo, and add authorized users to the sudo group

7. If possible, restrict network access to the SSH port or use a non-standard port number

