# SSH Configuration

Below is my preferred method of setting up my SSH keys.

### Generate Key Pair
On the local machine, execute the following.

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
If needed, make sure that `ssh-copy-id` is installed.  On OSX, it can be installed with [Homebrew](http://brew.sh/) with the command

```
brew install ssh-copy-id
```

Now execute the following to copy over the key.

```
ssh-copy-id -i ~/.ssh/localhost_remoteuser@remotehost_id_rsa.pub username@remotehost.domain.com
```

and enter your password when prompted.

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
