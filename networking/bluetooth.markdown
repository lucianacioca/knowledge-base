
# Bluetooth #

## Debian ##

Packages install :

~~~~~
apt-get install bluetooth obexftp
~~~~~

Check for bluetooth device :

~~~~~
hcitool dev
~~~~~

Scan for devices :

~~~~~
hcitool scan
~~~~~

Get device info :

~~~~~
hcitool info <macaddr>
~~~~~

Create bluetooth connection to device :

~~~~~
hcitool cc <macaddr>
~~~~~

Associate device (PIN exchange) :

~~~~~
bluez-simple-agent <bleutooth_device> <macaddr>
~~~~~

List devices :

~~~~~
bluez-test-device list
~~~~~

Discover services :

~~~~~
sdptool browse <macaddr>
~~~~~

### Browse filesystem of an Android Phone ###

- Install app _Bluetooth File Transfer_ from Google Play
- Discover services using `sdptool`, then get Channel ID of the `OBEX FTP` service
- Install package `obexfs`
- Mount your phone using this command :

~~~~~
obexfs -b <macaddr> -B <channelid> /mnt/android/
~~~~~

