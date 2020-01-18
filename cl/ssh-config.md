# SSH Configuration

Below is my preferred method of setting up my SSH keys.

### Generate Key Pair
On the local machine, execute the following where `-C` is a comment.

```
ssh-keygen -t rsa -b 4096 -C "username@remotehost.domain.com"
```

When prompted for the file name, write it as `~/.ssh/localhost_remoteuser@remotehost_id_rsa`.

### Setup SSH Config file
On the local machine create the file `~/.ssh/config`.  Below is a sample file.

```
# %l = local hostname
# %r = remote username
# %h = remote hostname
Host *
    Port 22
    ServerAliveInterval 60
Host remotehost
    HostName remotehost.domain.com remotehost
    User username
    IdentityFile ~/.ssh/%l_%r@%h_id_rsa
```

### Copy SSH Key

#### macOS
If needed, make sure that `ssh-copy-id` is installed.  On macOS, it can be installed with [Homebrew](http://brew.sh/) with the command

```
brew install ssh-copy-id
```

Now execute the following to copy over the key.

```
ssh-copy-id -i ~/.ssh/localhost_remoteuser@remotehost_id_rsa.pub username@remotehost.domain.com
```

and enter your password when prompted.

#### Windows
Copy the needed key using `scp` and then adjust needed permissions.  Everything below assumes PowerShell.

```powershell
cp C:\Users\yourUserName\.ssh\id_rsa.pub C:\Users\yourUserName\authorized_keys
```

On your host create the `.ssh` directory if it does not exist.

```sh
mkdir ~/.ssh/
```

Copy the file from windows to the remote host.

```powershell
scp authorized_keys user@remote:~/.ssh
```

Finally, back on the remote host make sure permissions are set correctly.

```sh
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

Of course test from Windows you can ssh without requiring a password.  Finally clean up by removing the `authorized_keys` file.

```powershell
Remove-Item C:\Users\yourUserName\authorized_keys
```

### Alternative
As an alternative, name the key as `~/.ssh/remoteuser@remotehost_id_rsa`.  This is necessary when working on my work computer as my hostname changes when I am working within the corporate network or outside the network.  

Thus, `~/.ssh/config` will mirror the sample file below.


```
# %r = remote username
# %h = remote hostname
Host *
    Port 22
    ServerAliveInterval 60
Host remotehost
    HostName remotehost.domain.com remotehost
    User username
    IdentityFile ~/.ssh/%r@%h_id_rsa
```

### Source
Adapted from http://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/.
Windows key copying from https://security.stackexchange.com/a/167953.
