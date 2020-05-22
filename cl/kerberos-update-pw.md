# Kerberos

## Kerberos - Create Password

What if you want to store your password for Kerberos authentication?  How do you store it for use in a script in order to run `kinit`?

Follow the directions below to create a `keytab`.  Then that `keytab` can be used for login purposes.  As an example, within your `bashcr` file, you can execute the following.

```bash
kinit -kt /home/username/.kerberos.keytab username@DOMAIN.COM
```

Why would you want to do this?  For instance, if you used key based login via `ssh` you may not explicitly login.  This allows for getting a Kerberos ticket upon login (regardless of the method to login).  However, this also would require one to maintain and regularly update their password as noted below.


## Kerberos - Other Commands

Other key commands 

```bash
# list
klist

# destroy
kdestroy
```

## Kerberos - Update Password

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
