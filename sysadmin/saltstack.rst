
SaltStack
=========

Useful URL
----------

- `Salt Stack Walkthrough <http://docs.saltstack.com/topics/tutorials/walkthrough.html>`_
- `Pillar Walkthrough <http://docs.saltstack.com/topics/tutorials/pillar.html>`_
- `States tutorial, part 1 <http://docs.saltstack.com/topics/tutorials/states_pt1.html>`_
- `How Do I Use Salt States ? <http://docs.saltstack.com/topics/tutorials/starting_states.html>`_
- `Jinja2 documentation <http://jinja.pocoo.org/docs/>`_
- `States tutorial, part 2 <http://docs.saltstack.com/topics/tutorials/states_pt2.html>`_
- `[T] States tutorial, part 3 <http://docs.saltstack.com/topics/tutorials/states_pt3.html>`_
- `[T] States tutorial, part 4 <http://docs.saltstack.com/topics/tutorials/states_pt4.html>`_
- `[T] State Enforcement <http://docs.saltstack.com/ref/states/index.html>`_
- `Salting your Django Stack <http://blog.gibbon.co/posts/2013-06-12-salting-your-django-stack.html>`_
- `Getting redundancy and scalability with multiple master servers <http://bencane.com/2014/02/04/saltstack-getting-redundancy-and-scalability-with-multiple-master-servers/#share>`_

Useful Salt functions
---------------------

==================== ==========================================================
Function             Description
==================== ==========================================================
cmd.run              Execute command
network.interfaces   Dump network configuration
pillar.items         List pillars on minion
service.get_all      List all system services
state.highstate      Run all states
sys.doc              Show all available functions
test.ping            Test connectivity
==================== ==========================================================

One-liners
----------

Execute state :

    salt host1 state.sls utils.vim

Development environment on Debian 7.0
-------------------------------------

Clone GIT repository : ::

    cd ~/git/
    git clone git://github.com/saltstack/salt.git
    cd salt

Install M2Crypto and Python header files : ::

    apt-get install python-m2crypto python-dev

Create and enable dedicated virtualenv : ::

    mkvirtualenv --system-site-packages salt
    workon salt

Install requirements : ::

    pip install pyzmq PyYAML pycrypto msgpack-python jinja2 psutil

Install test suite requirements : ::

    pip install -r dev_requirements_python27.txt

Using development environment
-----------------------------

Fetch latest changes from upstream develop : ::

    git pull upstream develop

Launch test suite : ::

    ulimit -n 3072
    ./setup.py test

Launch test suite for PostgreSQL : ::

./tests/runtests.py -n unit.modules.postgres_test -vv

Launch full test suite : ::

./tests/runtests.py --unit-tests

