tcpdump
=======

Capture only packets containing a SYN flag : ::

	tcpdump "tcp[tcpflags] & (tcp-syn) != 0"

