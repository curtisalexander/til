# Private on Github

Using the ideas found at Harry Robert's [blog post](https://24ways.org/2013/keeping-parts-of-your-codebase-private-on-github/), I use one local repo to sync with two Github remotes - one public and the other private.

For example, my [dotfiles](https://github.com/curtisalexander/dotfiles) contain a mix of files that need to be public and others that need to be private.  Thus, I create separate remotes on Github for each, managing them locally with branches.  This is in lieu of using something like [blackbox](https://github.com/StackExchange/blackbox) or [git-secret](https://github.com/sobolevn/git-secret), which encrypts your files within a repo, I am relying on the security and privacy of Github.

Below is an example with my dotfiles.  The most important thing to remember is this -- **if we `git clone` the repo on a new machine, we will need to setup remotes again!**  Failing to remember this fact is perhaps a reason why others choose to encrypt files in lieu of managing separate remotes via branches.

```bash
# create initial repo, which will be the public remote
mkdir -p ~/code/dotfiles && cd ~/code/dotfiles
git init
git remote add origin https://github.com/curtisalexander/dotfiles.git
echo "alias ll='ls -l'" >> bashrc
git add -A
git commit -m 'initial commit'
git push -u origin master

# create private remote
git checkout -b dotfiles-private
git remote add private https://github.com/curtisalexander/dotfiles-private.git
echo "hacktheplanet123" >> mypw
git add -A
git commit -m 'added mypw'
git push -u private dotfiles-private

# merge changes from `dotfiles-private` branch into `master`
#   appropriate when using the private remote as a storage for draft content
git checkout master
git merge dotfiles-private
git push
```
