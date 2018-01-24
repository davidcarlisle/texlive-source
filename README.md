
Converting a git checkout to a git svn-able repository
======================================================

This branch contains the necessary data to convert a git clone of this
repository into a git svn usable checkout.

The procedure is as follows

- clone this repository
- checkout the git-svn-data branch
- add the following code to your `.git/config`

````
[svn-remote "svn"]
        url = svn://USER@tug.org/texlive/trunk/Build/source
        fetch = :refs/remotes/git-svn
[svn]
        authorsfile = .git/usermap
````

- copy the file `usermap` included in this branch into the `.git` 
  directory
- create the directory `.git/svn/refs/remotes/git-svn/`, including all parents 
- copy the `index` file included in this branch into the above directory
- copy the file `git-svn` into `.git/refs/remotes/`
- call `git svn fetch`

The last command should *not* fetch the whole history, but only update
the index

````
$ git svn fetch
Rebuilding .git/svn/refs/remotes/git-svn/.rev_map.c570f23f-e606-0410-a88d-b1316a301751 ...
r1479 = 6f06d506596b6ae2009fa6c5734719f477d0acf2
r1480 = ffb7bc1ea9150c81b6bbf3232165c89f5cf71f0f
...
r46426 = 56366802bc50231f04cfa753fa58da73f02a67c7
r46427 = 609ab155005bfa5de48e60eb335df12228038891
Done rebuilding .git/svn/refs/remotes/git-svn/.rev_map.c570f23f-e606-0410-a88d-b1316a301751
$
````

