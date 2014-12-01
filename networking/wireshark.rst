Wireshark
=========

Filter all TCP SYN from 192.0.2.1 to TCP port 22 : ::

    tcp.flags.syn==1 and ip.src==192.0.2.1 and tcp.port==22 and tcp.flags.ack==0

