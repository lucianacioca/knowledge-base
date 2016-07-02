
======
Python
======

Interesting articles :

- `Drastically Improve Your Python: Understanding Python's Execution Model <http://www.jeffknupp.com/blog/2013/02/14/drastically-improve-your-python-understanding-pythons-execution-model/>`_

Useful modules :

- `Requests: HTTP for Humans <http://docs.python-requests.org/en/latest/>`_
- `A curated list of awesome Python frameworks, libraries and software <https://github.com/vinta/awesome-python>`_

Building Python from scratch
============================

Install important header files : ::

    apt-get install libbz2-dev zlib1g-dev libssl-dev libreadline-dev libsqlite3-dev libncurses5-dev

Download sources : ::

    wget https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tar.xz

Uncompress, build, install : ::

    tar xf Python-3.5.2.tar.xz
    cd Python-3.5.2
    ./configure --prefix=$HOME/.local/Python-3.5.2
    make
    make install

Create virtualenv using this new Python interpreter : ::

    mkvirtualenv -p $HOME/.local/Python-3.5.2/bin/python3 Python-3.5.2
    workon Python-3.5.2

Update pip and setuptools : ::

    pip install --upgrade setuptools pip

Install useful utils : ::

    pip install readline ipython pep8 pyflakes

Best practices
==============
- Follow PEP8 guidelines
- Follow PEP 257 guidelines (Docstring Conventions)

Misc
====

Get object type : ::

    type(object).__name__

