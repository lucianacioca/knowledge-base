
======
Python
======

Interesting articles :

- `Drastically Improve Your Python: Understanding Python's Execution Model <http://www.jeffknupp.com/blog/2013/02/14/drastically-improve-your-python-understanding-pythons-execution-model/>`_

Useful modules :

- `Requests: HTTP for Humans <http://docs.python-requests.org/en/latest/>`_

Building Python from scratch
============================

Install important header files : ::

    apt-get install libbz2-dev zlib1g-dev libssl-dev libreadline-dev libsqlite3-dev

Download sources : ::

    wget https://www.python.org/ftp/python/2.7.9/Python-2.7.9.tar.xz

Uncompress, build, install : ::

    tar xf Python-2.7.9.tar.xz
    cd Python-2.7.9
    ./configure --prefix=/opt/Python-2.7.9
    make
    make install

Create virtualenv using this new Python interpreter : ::

    mkvirtualenv -p /opt/Python-2.7.9/bin/python my_venv
    workon my_venv

Install useful utils : ::

    # If necessary, add --proxy=192.0.2.1:3128
    pip install readline ipython

