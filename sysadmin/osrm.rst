OSRM
====

Description
-----------

http://project-osrm.org/

*The Open Source Routing Machine (OSRM) is a C++ implementation of a
high-performance routing engine for shortest paths in road networks. It
combines sophisticated routing algorithms with the open and free road network
data of the OpenStreetMap (OSM) project.*

Installation on Debian Wheezy
-----------------------------

See also https://github.com/Project-OSRM/osrm-backend/wiki/Building-OSRM.

Install packages needed for compilation : ::

    apt-get install git libboost-dev gcc g++ make cmake libstxxl-dev \
    libxml2-dev libbz2-dev zlib1g-dev libzip-dev libboost-filesystem-dev \
    libboost-thread-dev libboost-system-dev libboost-regex-dev libboost-program-options-dev \
    libboost-iostreams-dev libgomp1 libpng-dev libprotoc7 libprotobuf-dev protobuf-compiler \
    liblua5.1-0-dev libluabind-dev pkg-config libosmpbf-dev libtbb-dev libboost-test-dev

Get last release on GitHub : https://github.com/Project-OSRM/osrm-backend/releases.

This howto has been tested using OSRM 4.4.0.

Go to the directory of the extracted tarball, then execute : ::

    mkdir -p build
    cd build
    cmake ..
    make

Create links to some profile files provided by the tarball : ::

    ln -s ../profiles/car.lua profile.lua
    ln -s ../profiles/lib/

Create a file called ``.stxxl`` containing : ::

    disk=stxxl.disk,15000,syscall

This will create a temporary 15 GB ``stxxl.disk`` file, so the corresponding
disk space should be available. Depending of the size of the OSM file, this
size could be adjusted.

Download OSM file (here a map of France) and convert it to a OSRM file (long!) : ::

    wget http://download.geofabrik.de/europe/france-latest.osm.bz2
    ./osrm-extract france-latest.osm.bz2

Then, precompute the data : ::

    ./osrm-prepare france-latest.osrm

Now, the big ``stxxl.disk`` file can be removed.

Create a ``server.ini`` file : ::

    Threads = 4
    IP = 0.0.0.0
    Port = 5000
    hsgrData=./france-latest.osrm.hsgr
    nodesData=./france-latest.osrm.nodes
    edgesData=./france-latest.osrm.edges
    ramIndex=./france-latest.osrm.ramIndex
    geometry=./france-latest.osrm.geometry
    fileIndex=./france-latest.osrm.fileIndex
    namesData=./france-latest.osrm.names

Finally, execute this binary and test the service : ::

    ./osrm-routed

Deployment (quick way)
^^^^^^^^^^^^^^^^^^^^^^

- Move the ``build`` directory into ``/usr/local``.
- Move the ``server.ini`` file into ``/etc/osrm/``.
- Specify absolute path in ``server.ini``.
- Launch OSRM with : ::

    /usr/local/osrm/osrm-routed -c /etc/osrm/server.ini

