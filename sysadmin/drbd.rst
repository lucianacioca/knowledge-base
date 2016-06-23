DRBD
====

Speed up synchronization temporarily (execute it on the ``SyncTarget`` host,
example for using a 30M/s bandwidth for resource ``res``) : ::

    drbdadm disk-options --c-plan-ahead=0 --resync-rate=30M res

