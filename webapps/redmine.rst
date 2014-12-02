
Redmine
=======

Installation on Debian Wheezy
-----------------------------

Install required dependencies : ::

    apt-get install ruby ruby-dev rubygems libmagickwand-dev sqlite3

**The following instructions can be executed as a regular user.**

Download and extract Redmine tarball (here ``redmine-2.6.0.tar.gz``), then move
into the extracted directory.

Configure database access in ``config/database.yml`` (examples given in
``config/database.yml.example``).

Execute : ::

    gem install --user-install bundler rake
    ~/.gem/ruby/1.9.1/bin/bundle install --path ~/.gem --without development test
    ~/.gem/ruby/1.9.1/bin/rake generate_secret_token
    ~/.gem/ruby/1.9.1/bin/rake db:migrate RAILS_ENV="production"

Launch the WEBrick server : ::

    ruby script/rails server -e production

