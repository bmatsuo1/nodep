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

At 9805c4da6f164857a4e32dbfe83767f1118c9ad4 godep attempts to vendor the
intrarepository dependencies and fails.

```
# cd /home/bmatsuo/src/github.com/bmatsuo1/nodep/go-uuid/uuid; hg diff -r 7dda39b2e7d5e265014674c5af696ba4186679e9+
hg: parse error at 41: not a prefix: end
godep: dirty working tree (please commit changes): /home/bmatsuo/src/github.com/bmatsuo1/nodep/go-uuid/uuid
godep: error loading dependencies
```
