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

Misc
----

Load an improved shell with all models pre-loaded : ::

    python manage.py shell_plus

Display all SQL queries : ::

    python manage.py shell_plus --print-sql

Install ``django-extensions``, then these commands (among others) become
available : ::

    python manage.py runserver_plus
    python manage.py shell_plus
    python manage.py graph_models <APPNAME>
    python manage.py print_settings
    python manage.py set_fake_passwords
    python manage.py show_urls

Logging
-------

Default Django logging is defined in ``django/utils/log.py``.

