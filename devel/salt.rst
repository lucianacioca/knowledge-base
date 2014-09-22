
Salt
====

Make a contribution
-------------------

Reference : `Contributing <http://docs.saltstack.com/en/latest/topics/development/contributing.html>`_.

Create a fork on Github and clone it.

If the clone already exists, fetch new updates from Salt upstream repository : ::

    git remote add upstream git@github.com:saltstack/salt.git
    git pull --rebase upstream develop

Checkout a dedicated branch for the change : ::

    git checkout -b fix-example

Now the change can be made, commited, and pushed : ::

    git ci -a
    git push origin fix-example

On your Github fork, select the branch, and click "Compare & pull request".

Check the diff, and confirm by clicking "Create pull request".

