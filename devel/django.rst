Django
======

Ressources
----------

- `Effective Django <http://effectivedjango.com/tutorial/>`_

Project init
------------

Create virtualenv.

Install Django : ::

    pip install Django

Fixtures
--------

Dump SQL data into fixture file : ::

    mkdir app/fixtures
    python manage.py dumpdata --format=json --indent=4 >app/fixtures/test.json

Load fixture : ::

    python manage.py loaddata test.json

