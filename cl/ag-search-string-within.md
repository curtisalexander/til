# `ag` - Search for String Within a File

Search within files for the string 'mystring' with options
* ignoring case
* files of type `.sas`
* recursively beginning in the current folder 

```
ag 'mytextstring' -i -G .sas > ~/ag_results.txt
```
