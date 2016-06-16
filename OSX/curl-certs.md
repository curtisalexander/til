# cURL and Certificates
I have need to utilize a custom certificate on my OSX machine.  In order to make some software work, I have to set the environment variables `SSL_CERT_DIR` and `SSL_CERT_FILE`.  Unfortunately, when these environment variables are set on OSX, `curl` doesn't work as expected.

One workaround is [similar](homebrew-conda-certs.md#homebrew) to they way in which I intercept the call to `brew`.  Below is an example where I remove the environment variables from the executing environment and then make a system call to `curl`.

In Python, whenever `os` is imported a Python dictionary, `os.environ`, is created containing all environment variables.  In the `del` statement below, I am deleting the environment variables from the dictionary `os.environ`.  When I make a call to the shell using `subprocess`, the environment variables within `os.environ` are passed along (which will exclude `SSL_CERT_DIR` and `SSL_CERT_FILE`).  But after the script completes, the environment variables have not been permanently delted.  The `del` operation in Python is **not** equivalent to `unset` in a shell script.

```
#!/usr/bin/env python

import os
import shlex
import subprocess

# delete environment variables
# this is necessary because of the way curl works on OSX

del os.environ['SSL_CERT_DIR']
del os.environ['SSL_CERT_FILE']

cmd = 'curl --ntlm -s --netrc https://host.com/requiring/ntlm/authentication/default.aspx'
args = shlex.split(cmd)

p = subprocess.run(args,
                   stdout = subprocess.PIPE,
                   stderr = subprocess.PIPE,
                   universal_newlines = True)

# do something with p, the result of the call to curl
# for example, use Beautiful Soup to parse the resulting html document
import bs4
soup = bs4.BeautifulSoup(p.stdout, 'html.parser')
```
