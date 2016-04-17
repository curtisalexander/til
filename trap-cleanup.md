# Trap and Cleanup After a Shell Script

Courtesy [Aaron Maxwell](http://redsymbol.net/articles/bash-exit-traps/).

An exit trap can be utilized within a shell script to cleanup after completion -- will execute if the script exits for **any** reason.

```sh

function finish {
    # cleanup code
}

trap finish EXIT
```

Another pattern is to trap errors and interruptions in order to print the line number where an error occurred.

```sh
trap 'echo Error: $0:$LINENO stopped; exit 1' ERR INT
```
