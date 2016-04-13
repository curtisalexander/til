# Tree Replacement

If `tree` is not available (say on a production Linux server that does not connect to the outside), then you can create your own quasi-tree functionality using the below.

```bash
if [ -n "$1" ]; then
    find "$1" -print | sort | sed -e '/^\.$/d' -e 's/[^-][^\/]*\//--/g' -e 's/^/  /' -e 's/-/|/'
else
    find . -print | sort | sed -e '/^\.$/d' -e 's/[^-][^\/]*\//--/g' -e 's/^/  /' -e 's/-/|/'
fi
```
