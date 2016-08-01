# Kerberos - Update Password

How to update Kerberos keytab file after AD password is updated?  Delete the keytab and create a new keytab - there doesn't appear to be a mechanism for inplace updates.

There may be a better way to do this by creating a temporary file and swapping out the files.  To be researched later.

```bash
# backup keytab
$ mv ~/.kerberos.keytab ~/.kerberos.keytab.bak

# drop into ktutil
$ ktutil

# below are commands to enter within ktutil

# add new entry
ktutil: addent -password -p username@DOMAIN.COM -k 1 -e rc4-hmac

# write keytabs - ~/ will not expand to $HOME
ktutil: write_kt /home/username/.kerberos.keytab

# quit
ktutil: quit
```
