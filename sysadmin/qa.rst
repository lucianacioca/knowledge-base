
=================
Quality assurance
=================

This is a list of items to check on a Debian server.

=================            ====================================
Check point                  Desired state
=================            ====================================
NTP                          Synced on debian.pool.ntp.org + Nagios check
Backup                       Daily incremental backup (system + data)
Monitoring                   Nagios system check
SSH Security                 User login only by key
Updates notification         Nagios check
Root access                  Only via sudo or without-password (for backups)
Root password                Disabled, or very complex
Admin mail                   Admin receive root@ e-mails via local MTA
Kernel                       Minimal kernel is built without module support
Firewall                     IPtables enabled with secure rules set
Storage                      RAID monitored by Nagios
Metrics                      Munin enabled and available
Documentation                Written and available
=================            ====================================

