# `rg`

Searches using [ripgrep](https://github.com/BurntSushi/ripgrep).  Examples below tested on `rigpgrep 0.3.2`.

### Windows
**Quotes**<br>
Within the Windows command prompt, quoting must be done using double quotes -- `"*.sas"`.

**UNC paths**<br>
To search within a [UNC network path](https://en.wikipedia.org/wiki/Path_(computing)#MS-DOS.2FMicrosoft_Windows_style), the easiest method is to first `cd` into the directory.  One may either map the drive manually or use the [`pushd`](http://superuser.com/a/399885) command to automatically map the drive and `cd` into it.

```
pushd \\some\network\path\dir
```

### Defaults
* if pattern lowercase, then case insensitive
* recursive
* filenames as headers
* line numbers
* ignore binary files

### Search examples

**search context:** within files<br>
**options:**<br>
* specific extension

```
rg --type-add "sas:*.sas" -tsas "proc means"
```

**search context:** filenames<br>
**options:**<br>
* specific extension

```
rg --type-add "sas:*.sas" -tsas --files
```

**search context:** filenames<br>
**options:**<br>
* glob

```
rg -g *proposal* --files
```
