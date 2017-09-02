# Homebrew and Conda Certficates
I have need to utilize a custom certificate when making https requests on my macOS machine.  Because of this, I often have to adjust various environment variables.  But in order to be able to use [homebrew](http://brew.sh) as well as [conda](http://conda.pydata.org/miniconda.html) simultaneously, I have to resort to some trickery.

## conda
There are two different ways in which I use conda.

### conda install
One is to simply install something from one of the default channels (or potentially conda-forge).

```
conda install scikit-learn
```

The above will run if I make a change to my `~/.condarc` file and so long as I have imported my custom certificate into my system keychain.  

Add the following line to `~/.condarc`.

```
ssl_verify: ~/.cert/ca-bundle.crt
```

In order to import my custom certificate into my system keychain, I execute the following.

```
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain ~/.cert/ca-bundle.pem
```

### conda skeleton
Sometimes I have to install a package that is only available on [PyPI](https://pypi.python.org/pypi).  For this, I use a formula similiar to below (I prefer managing everything through `conda` rather than using `pip`).

```
conda skeleton pypi keras
conda build keras
conda install --use-local keras
```

But when `conda skeleton` is run, I will receive SSL errors that I never received when running `conda install ...`.  In order to correct, I have to set the environment variables below in my `~/.zshrc` file.

```
export SSL_CERT_DIR="~/.cert"
export SSL_CERT_FILE="~/.cert/ca-bundle.crt"
```

With these changes, I am able to successfully run `conda skeleton`.

## homebrew
Unfortunately, if I have the environment variables `SSL_CERT_DIR` and `SSL_CERT_FILE` set then homebrew will not work; it will throw SSL errors.  This [issue](https://github.com/Homebrew/legacy-homebrew/issues/43154) confirms the need to have the SSL environment variables unset.

Because one command line tool needs the environment variables and another doesn't, I hacked a solution.  In my `$PATH`, my personal `~/bin` directory comes before `/usr/local/bin` which is where the `brew` command is located.  Within `~/bin`, I created a shell script named `brew`.  This script intercepts calls to `brew`.  The script backs up the environment variables, unsets the environment variables, calls `/usr/local/bin/brew` with the remaining arguments from the command line (`$*`) and then sets the environment variables back to what they were originally.  Below is the `~/bin/brew` script.

```
#!/usr/bin/env bash

PRIOR_SSL_CERT_DIR="${SSL_CERT_DIR}"
PRIOR_SSL_CERT_FILE="${SSL_CERT_FILE}"

unset SSL_CERT_DIR
unset SSL_CERT_FILE

/usr/local/bin/brew "${*}"

export SSL_CERT_DIR="${PRIOR_SSL_CERT_DIR}"
export SSL_CERT_FILE="${PRIOR_SSL_CERT_FILE}"
```
