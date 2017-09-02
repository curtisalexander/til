# homebrew - Check If a Package Is Installed
To check if a [Homebrew](http://brew.sh) package is installed, execute the following.  The example below checks to see if `fzf` is installed.

```sh
brew ls --versions fzf
```

To utilize within a script, use with an `if` statement.

```sh
if [ -z "$(brew ls --versions fzf)" ]; then
    echo 'the package fzf is not installed'
else
    echo 'the package fzf is installed'
fi
```
