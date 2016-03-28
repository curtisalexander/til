# `less` Instead Of `tail`

Rather than using `tail` to review a log
```
tail -f log/mylog.log
```

use `less`
```
less +F log/mylog.log
```

### Usage
* `Ctrl-C` drops into editing mode
* Scroll using vim commands - `j`, `k`, `l`, `h`
* Search using `/pattern`
* `Shift+F` returns back to tailing the file
