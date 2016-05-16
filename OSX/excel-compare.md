# ExcelCompare on OSX
In order to use [ExcelCompare](https://github.com/na-ka-na/ExcelCompare/) on OSX, the wrapper script `excel_cmp` needs to be updated.

The command `readlink -f` does not exist on OSX.  Thus, a `realpath` alternative needs to be used in order to resolve symbolic links appropriately.  See [bash - Bash realpath Function](../cl/bash-realpath.md) for information on `realpath` on OSX.

Below is the re-written `excel_cmp` file that works on OSX.

```bash
#!/usr/bin/env sh

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

if [ -L $0 ];then
  dir="$(realpath "$0" | xargs dirname)"
else
  dir="$(dirname "$0")"
fi

java -ea -Xmx512m -cp "$dir/dist/*" com.ka.spreadsheet.diff.SpreadSheetDiffer "$@"
```
