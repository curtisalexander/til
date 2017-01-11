# `rg`

Various searches using [ripgrep](https://github.com/BurntSushi/ripgrep).  Examples below are for `rigpgrep 0.3.2`.

## Windows
Within the Windows command prompt, quoting must be done using double quotes -- `"*.sas"`.

## Defaults
* if pattern lowercase, then case insensitive
* recursive

## Search examples

**search context:** within files
**options:**
* specific extension

```
rg --type-add "sas:*.sas" -tsas "proc means"
```

**search context:** filenames
**options:**
* specific extension

```
rg --type-add "sas:*.sas" -tsas --files
```
