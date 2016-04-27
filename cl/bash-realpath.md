# bash `realpath` function
In order to find the directory a script is running from, it is necessary to resolve symbolic links.  On Linux, this can be accomplished with `realpath -m`.  The `-m` switch recursively resolves symlinks in order to provide the true `realpath`.

Unfortunately on OS X, there is not a `-m` switch for `realpath`.  The BSD version of `realpath` will only resolve a single symbolic link.  Thus, this is resolved using the while loop below.

### Function
Below is taken from a Stack Overflow answer from [Geoff Nixon](http://stackoverflow.com/a/18443300).

**Note:** The `realpath` returned does **not** have a trailing slash.

```bash
realpath() {
    local _PWD="$(pwd)"
    cd "$(dirname "$1")"
    local _LINK="$(readlink "$(basename "$1")")"
    while [ "${_LINK}" ]; do
        cd "$(dirname "${_LINK}")"
        _LINK="$(readlink "$(basename "${1}")")"
    done
    local _REALPATH="${PWD}/$(basename "${1}")"
    REALPATH="${_REALPATH%/}"
    cd "${_PWD}"
    echo "${REALPATH}"
}
```

### Usage
Within a bash script, utilize in the following way.

```bash
SCRIPT="$(realpath "$0")"
SCRIPT="$(dirname $(realpath "$@"))"
```

For an example, see [rproject-init](https://github.com/curtisalexander/rprofile-init/blob/master/rprofile-init).
