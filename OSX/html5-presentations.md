# HTML5 Presentations

### Problem
I would like to project and present an HTML5 presentation (such as a [shower](https://shwr.me) or an [rmdshower](https://github.com/MangoTheCat/rmdshower)) fullscreen within a browser.  Even if I set the browser to be fullscreen, I still have the address bar and tab bar to contend with.  These can be turned off within the browser but I can never recall how to do so.

### Solution
Instead of opening a local HTML5 presentation via double-click (or via `open` on the command line), I open the presentation in `app` mode.  Below is a simple shell script I use to open an HTML5 presentation from the command line in a fullscreen.

```bash
#!/usr/bin/env bash

set -e

# realpath - works on OSX and Linux
realpath() {
    local _PWD="$(pwd)"
    cd "$(dirname "${1}")"
    local _LINK="$(readlink "$(basename "${1}")")"
    while [ "${_LINK}" ]; do
        cd "$(dirname "${_LINK}")"
        _LINK="$(readlink "$(basename "${1}")")"
    done
    local _REALPATH="${PWD}/$(basename "${1}")"
    REALPATH="${_REALPATH%/}"
    cd "${_PWD}"
    echo "${REALPATH}"
}

# presentation
PREZ="${1}"

# n = non-zero length string
if [ -n "${PREZ}" ]; then
    PREZ_PATH=$(realpath "${PREZ}")
    /Applications/Vivaldi.app/Contents/MacOS/Vivaldi --app=file://${PREZ_PATH}
else
	echo -e "\nUsage:"
	echo -e "  $(basename $0) presentation.html\n"
fi
```
