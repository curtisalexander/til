# `rg`

Searches using [ripgrep](https://github.com/BurntSushi/ripgrep).  Examples below tested on `rigpgrep 0.4.0`.

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
<br><br>
## Search examples
<br><br>
**search context:** within files<br>
**options:** specific extension
<br>
```
rg --type-add "sas:*.sas" -tsas "proc means"
```
<br><br>
**search context:** within files<br>
**options:** specific extension, redirect stdout to file
<br>
```
rg --heading --line-number --type-add "sas:*.sas" -tsas "proc means" > proc_means_search_results.txt
```
<br><br>
**search context:** filenames<br>
**options:** specific extension
<br>
```
rg --type-add "sas:*.sas" -tsas --files
```
<br><br>
**search context:** filenames<br>
**options:** glob
<br>
```
rg -g "*proposal*" --files
```
<br><br>
**search context:** filenames<br>
**options:** specific extension, glob
<br>
```
rg -g "*final*" --files --type-add "prez: *.{pdf,pptx}" -tprez
```
