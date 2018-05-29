===
GIT
===

Web ressources
==============
- `Everyday GIT With 20 Commands Or So <https://www.kernel.org/pub/software/scm/git/docs/everyday.html>`_
- `Git Magic <http://www-cs-students.stanford.edu/~blynn/gitmagic/index.html>`_
- `Pro Git book <http://www.git-scm.com/book>`_

Documentation
=============
- Git revisions : `man gitrevisions`

Command line operations
=======================

Define username *bob* to authenticate to http://git.example.com : ::

    git config credential.http://git.example.com.username bob

Track remote branch origin/master for local branch master : ::

    git branch --set-upstream master origin/master

Create and checkout a local branch : ::

    git checkout -b local-branch

Push local branch to remote ``origin`` : ::

    git push --set-upstream origin local-branch

Cancel last commit : ::

    git reset --soft HEAD^

Delete remote branch : ::

    git push origin :remote_branch

Delete stale remote-tracking branches : ::

    git remote prune origin

List and filter files managed by git : ::

    git ls-files

Search among managed files : ::

    git grep <PATTERN>

Display commit by commit message : ::

    git show :/Message

Add prefix to commit messages using sed : ::

    git filter-branch --msg-filter "sed 's/^/PREFIX /'" HEAD ^f78f088^

Convert SVN repository to GIT
=============================

Install ``svn-all-fast-export``.

Create an ``identity`` file containing mapping between SVN and GIT accounts.
Example : ::

    john = John Doe <john@example.com>

Create a rule file describing how SVN data should be organized in the GIT
repository : ::

    create repository repo.git
    end repository
    match /trunk/
      repository repo.git
      branch master
    end match

Execute ``svn-all-fast-export`` : ::

    svn-all-fast-export --rules RULEFILE --identity-map IDENTITYFILE /path/to/svnrepo

