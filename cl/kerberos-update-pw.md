# Kerberos - Update Password

How to update Kerberos keytab file after AD password is updated?  Delete entry and create a new entry - there doesn't appear to be a mechanism for inplace updates.

```bash
# drop into ktutil
$ ktutil

# below are commands to enter within ktutil

# read keytab file
ktutil: read_kt /home/username/.kerberos.keytab

# list keytabs
ktutil: list 

# delete slot 1 entry
ktutil: delent 1

# add new entry
ktutil: addent -password -p username@DOMAIN.COM -k 1 -e rc4-hmac

# write keytabs 
ktutil: write_kt /home/username/.kerberos.keytab

# quit
ktutil: quit
```
