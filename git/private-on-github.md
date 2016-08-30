# Private on Github

## Background
Using the ideas found at Harry Robert's [blog post](https://24ways.org/2013/keeping-parts-of-your-codebase-private-on-github/), I use one local repo to sync with two Github remotes - one public and the other private.

For example, my [dotfiles](https://github.com/curtisalexander/dotfiles) contain a mix of files that need to be public and others that need to be private.  Thus, I create separate remotes on Github for each, managing them locally with branches.  This is in lieu of using something like [blackbox](https://github.com/StackExchange/blackbox) or [git-secret](https://github.com/sobolevn/git-secret), which encrypt your files within a repo.  To protect my files I am not relying on encryption but am relying on the security and privacy of private repositories on Github.

## Details
Before getting to the details, a brief warning.

### WARNING
If you use the methodology I outline below, then the most important thing to remember is this

> If you `git clone` the private/public repo on a new machine, you will need to setup your remote again!

Failing to remember this fact is perhaps a reason why others choose to encrypt files in lieu of managing separate remotes via branches.

---

Below is the methodology I use to setup and manage my dotfiles.

```bash
# create the initial repo, which will be the public remote
# in this example, public equates to the master branch
mkdir -p ~/code/dotfiles && cd ~/code/dotfiles
git init
git remote add origin https://github.com/curtisalexander/dotfiles.git
echo "alias ll='ls -l'" >> bashrc
git add -A
git commit -m 'initial commit'
git push -u origin master

# create the private remote by creating a separate branch with a different
#   remote than the public remote
git checkout -b dotfiles-private
git remote add private https://github.com/curtisalexander/dotfiles-private.git
echo "hacktheplanet123" >> mypw
git add -A
git commit -m 'added mypw'
git push -u private dotfiles-private

# merge changes from the master branch into the dotfiles-private branch
#   push changes back up to the remote (Github)
git checkout dotfiles-private
git merge master
git push

# merge changes from the dotfiles-private branch into the master branch
# WARNING - this is only  appropriate when using the private remote as 
#    storage for draft content
# IT IS NOT APPROPRIATE if you are trying to keep information private between your
#   public and private remotes
git checkout master
git merge dotfiles-private
git push
```

## Sync Private with Public 
Following up on Jenny Bryan's [tweet](https://twitter.com/JennyBryan/status/770526265623273472), I have outlined how one could use a [git post-commit hook](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) to keep a private branch in sync with the public.  The scenario assumed is that you would like to have your private repository mirror your public repository.  The only difference is that within your private branch you would like to keep a file or set of files private.

The example below is derived from an earlier TIL I wrote - [Sync master & gh-pages](git/sync-master-gh-pages.md).

To begin, within your public branch create the file `.git/hooks/post-commit`.  In my example, my public branch is actually my `master` branch.

```bash
# make sure you are adding the file within the public branch
#   for me, my public branch is the master branch
cd ~/code/dotfiles
git checkout master

# now actually make open and edit the file .git/hooks/post-commit
{vim,emacs,nano,code,subl,atom} .git/hooks/post-commit
```

The post-commit hook is actually just a shell script that executes after every commit on the `master` branch.  Below is the contents of `.git/hooks/post-commit`.

```bash
#!/bin/sh

# checkout the private branch
git checkout dotfiles-private

# don't immediately commit
git merge --no-commit master

# use the last commit message on the master branch as the commit
#   message for the merge
git commit -m "$(git log -1 master --pretty=%B)"

# checkout master to revert back to original state
git checkout master
```

Ensure that the newly create files, `.git/hooks/post-commit` is executable as it is in fact a shell script.

```bash
chmod +x .git/hooks/post-commit
```

Below is an example of a simple change and testing that files are synced between branches.

```bash
# make the change on master
git checkout master
echo "alias la='ls -a'" >> bashrc
git add -A
git commit -m 'add ls -a as an alias to bashrc'

# test that the change on master was synced between it and the private branch
# stdout should be blank as there are not any differences
diff <(tail -5 bashrc) <(git checkout --quiet dotfiles-private; tail -5 bashrc; git checkout --quiet master)
```

Finally, I have not determined a manner to push both the public and private branches to their respective remotes simultaneously.  But to push both is as simple as executing the following.

```bash
git push origin master
git push private dotfiles-private
```
