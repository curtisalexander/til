# `sudo` within Bash Scripts

Often, I will write a `bash` script that is a wrapper for other scripts.  The other scripts within the wrapper require `sudo` (usually for updating applications / packages).  Thus, to utilize my `sudo` password later in the script, I ask for the password up front.

```bash
read -s -p "Please provide password for sudo: " sudopw
echo
```

Then to utilize the password.

```bash
echo $sudopw | sudo -S ~/path/to/my/sudo-script
```
