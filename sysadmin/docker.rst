
Docker
======

Ubuntu 15.10 ::

    apt install docker.io

Add your personal user to the ``docker`` group.

Check everything OK ::

    $ docker info
    Containers: 0
    Images: 0
    Storage Driver: aufs
     Root Dir: /var/lib/docker/aufs
     Backing Filesystem: extfs
     Dirs: 0
     Dirperm1 Supported: true
    Execution Driver: native-0.2
    Kernel Version: 4.2.0-21-generic
    Operating System: Ubuntu 15.10
    CPUs: 4
    Total Memory: 15.5 GiB
    Name: neutrino
    ID: VOY5:EX2R:L55R:3IQO:FFLZ:TIOM:EBCJ:OCKV:AROM:75AY:XHVP:WJZG
    WARNING: No swap limit support

Pull Ubuntu image ::

    docker pull ubuntu

