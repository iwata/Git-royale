Git royale
========

Summary
---------------

1. A successful branch management
1. ``git-flow``
1. Some problems
1. Solution
    * ``-R | --remote`` option
1. Conclusion
1. Do you have any questions?
    * with IRC(#git)
1. One more thing
    * ``git now``



A successful branch management
-------------------

* [http://nvie.com/posts/a-successful-git-branching-model/](http://nvie.com/posts/a-successful-git-branching-model/)
    * [Japanese](http://keijinsonyaban.blogspot.com/2010/10/successful-git-branching-model.html)

![branch management](http://nvie.com/img/2009/12/Screen-shot-2009-12-24-at-11.32.03.png)

### Why git?

* Subversion is dead.
* Branching and merging are no longer something to be afraid of

### Two main branches
* Master
    * A production-ready state
* Develop
    * for the next release

![Two main branches](http://nvie.com/img/2009/12/bm002.png)

### Supporting three topic branches

* Feature
* Release
* Hotfix

### Feature branches

branch off | merge back
-----------|-----------
delevelp   | develop

![Feature branches](http://nvie.com/img/2009/12/fb.png)

### Release branches

branch off | merge back
-----------|-----------
develop   | develop and master

![Release branches](https://github.com/iwata/Git-royale/raw/master/rb.png)

### Hotfix branches

branch off | merge back
-----------|-----------
master   | develop and master

![Hotfix branches](http://nvie.com/img/2010/01/hotfix-branches1.png)

## ``git-flow``
Git extensions to provide high-level repository operations for the branching model

[https://github.com/nvie/gitflow](https://github.com/nvie/gitflow)

    $ brew install git-flow

### Init

    $ git checkout -b develop origin/master
    $ git flow init

### Feature branches

* Start feature branch

        $ git flow feature start smartphone-version

    This means:

        $ git checkout -b feature/smartphone-version develop

* Finish feature branch

        $ git flow feature finish smartphone-version

    This means:

        $ git checkout develop
        $ git merge --no-ff feature/smartphone-version
        $ git branch -d feature/smartphone-version

### Release branches

* Start release branch

        $ git flow release start 1.0

    This means:

        $ git checkout -b release/1.0 develop

* Finish release branch

        $ git flow release finish 1.0

    This means:

        $ git checkout master
        $ git merge --no-ff release/1.0
        $ git tag -a 1.0
        $ git checkout develop
        $ git merge --no-ff release/1.0
        $ git branch -d release/1.0

### Hotfix branches

* Start hotfix branch

        $ git flow start 1.1

    This means:

        $ git checkout -b hotfix/1.1

* Finish hotfix branch

        $ git flow finish 1.1

    This means:

        $ git checkout master
        $ git merge --no-ff hotfix/1.1
        $ git tag -a 1.1
        $ git checkout develop
        $ git merge --no-ff hotfix/1.1
        $ git branch -d hotfix/1.1

## Some problems

``git-flow`` dose not concern for remote repository.
Therefore, you need to sync to remote repository with hands.

## Solution

Add ``-R | --remote`` option

[https://github.com/iwata/gitflow](https://github.com/iwata/gitflow)

    $ brew install https://github.com/iwata/gitflow/raw/master/git-flow.rb

### Feature branches

* Start feature branch

        $ git flow feature start -R smartphone-version2

    This means:

        $ git checkout -b feature/smartphone-version2 develop
        $ git push -u origin feature/smartphone-version2

* Finish feature branch

        $ git flow feature finish -R smartphone-version2

    This means:

        $ git checkout develop
        $ git merge --no-ff feature/smartphone-version2
        $ git branch -d feature/smartphone-version2
        $ git push origin develop
        $ git push origin :feature/smartphone-version2

### Release branches

* Start release branch

        $ git flow release -R start 2.0

    This means:

        $ git checkout -b release/2.0 develop
        $ git push -u origin release/2.0

* Finish release branch

        $ git flow release finish -R 2.0

    This means:

        $ git checkout master
        $ git merge --no-ff release/2.0
        $ git tag -a 2.0
        $ git checkout develop
        $ git merge --no-ff release/2.0
        $ git branch -d release/2.0
        $ git push origin master
        $ git push origin develop
        $ git push --tags
        $ git push origin :release/2.0

### Hotfix branches

* Start hotfix branch

        $ git flow start -R 2.1

    This means:

        $ git checkout -b hotfix/2.1
        $ git push -u origin hotfix/2.1

* Finish hotfix branch

        $ git flow finish -R 2.1

    This means:

        $ git checkout master
        $ git merge --no-ff hotfix/2.1
        $ git tag -a 2.1
        $ git checkout develop
        $ git merge --no-ff hotfix/2.1
        $ git branch -d hotfix/2.1
        $ git push origin master
        $ git push origin develop
        $ git push --tags
        $ git push origin :hotfix/20111201-1234


## Conclusion

1. Subversion is dead.
1. ``git-flow`` is very useful.
    * But it has some problems.
1. To use advanced ``git-flow`` is the solution.
    * Add ``-R | --remote`` option

## One more thing

``git-now`` is a command-line tool for light and temporary commit.
It commits with a log message from time now and diff.

* [An original git-now idea](http://d.hatena.ne.jp/sinsoku/20101208/1291770514) (by [Toshiyuki Kawanishi](https://github.com/toshi-kawanishi))
* [https://github.com/iwata/git-now](https://github.com/iwata/git-now)

        $ brew install git-now
        $ brew install --zsh-completion git-now
