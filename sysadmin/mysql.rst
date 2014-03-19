
=====
MySQL
=====

Replication
===========

Launch replication
------------------

Dump all databases on master : ::

    mysqldump -A --add-drop-database --master-data >/data/tmp/all.sql

Then transfer and load the dump on the slave.

Finally, use replication infos in top of the dump file to execute the "CHANGE
MASTER" statement.

Operations
----------

Skip next query on slave : ::

    mysql> SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1;
    mysql> START SLAVE;

Tools
=====

- `Percona Toolkit for MySQL <http://www.percona.com/software/percona-toolkit>`_

