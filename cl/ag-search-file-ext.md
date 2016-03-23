# `ag` - Search for File Extension

Recursively search for all files with a particular extension in the background (assumes it will take quite some time).  For example, search for all files with a `.py` Python extension.

```
nohup ag -g '.\.py' -i --depth -1 --stats /dir/to/be/searched > python_search_results.txt &
```
