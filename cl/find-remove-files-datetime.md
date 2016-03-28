# `find` - Remove Files Based on Datetime

Search through a directory and remove files that are newer than March 28th at 11:00 am.

```
find . -type f -newermt "Mar 28 11:00" | xargs rm -f
```

Search through a directory and remove files that are older than March 28th at 11:00 am.

```
find . ! \( -type f -newermt "Mar 28 11:00" \) | xargs rm -f
```
or
```
find . -type f -not -newermt "Mar 28 11:00" | xargs rm -f
```
