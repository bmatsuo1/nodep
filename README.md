this repo merely contains an example program that had its godep build broken by
a recent commit.

https://github.com/tools/godep/commit/9805c4da6f164857a4e32dbfe83767f1118c9ad4

**NOTE:** The `go-uuid` directory in this repo is from
https://code.google.com/p/go-uuid.  It has merely been cloned and commited to
this repo.  Following that, customization was added to the library and
committed to git (not commited to `hg`).

The following command exhibits previously unexpected behavior (when cloned at
`$GOPATH/src/github.com/bmatsuo1/nodep`)

    cd mycmd && godep save ./src/...

Prior to 9805c4da6f164857a4e32dbfe83767f1118c9ad4 this command was a noop
because all dependencies to mycmd are within this repo.

At 9805c4da6f164857a4e32dbfe83767f1118c9ad4 the intrarepository dependecy is
copied into the godep workspace and `hg` commands are run which end up
modifying files and dirtying the repository. The following `git status` output
summarized how the repository is modified.

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   ../go-uuid/.hg/dirstate
    modified:   Godeps/Godeps.json

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    ../go-uuid/.hg/cache/tags
    Godeps/_workspace/src/

no changes added to commit (use "git add" and/or "git commit -a")
```
