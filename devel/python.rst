
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

    pip install readline ipython pep8 pyflakes pip-tools pipdeptree

Best practices
==============
- Follow PEP8 guidelines
- Follow PEP 257 guidelines (Docstring Conventions)
- For Python 2/3 compat, use :
    - ``from __future__ import unicode_literals``
    - ``from __future__ import print_function``
- Formatting : see https://pyformat.info/

Misc
====

Get object type : ::

    type(object).__name__

Python tools
============

Display tree of PIP packages : ::

    pipdeptree

Update packages exactly as specified in a requirements file (uninstalling
some packages if necessary) : ::

    pip-sync requirements.txt

Install PIP package in editable mode (example with django-compressor) : ::

    git clone git@github.com:django-compressor/django-compressor.git
    pip install -e django-compressor
    vim django-compressor/[...]   # Time to code/debug

Uninstall package in editable-mode (no specificity) : ::

    pip uninstall django-compressor

