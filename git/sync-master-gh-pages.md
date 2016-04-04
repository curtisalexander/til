# Sync master & gh-pages

The following keeps a single html file within the `master` branch of a repo synced with the `index.html` file within the `gh-pages` branch.

For example, I have the file `rmarkdown-syntax-highlighting.html` within the [repo](https://github.com/curtisalexander/rmarkdown-syntax-highlighting) of the same name.  This is the file that I would like to serve at http://curtisalexander.github.io/rmarkdown-syntax-highlighting/.  In order to do so, I copy this file into the `gh-pages` branch of the repo and rename the file as `index.html`.

In order to achieve this, I create the file `.git\hooks\post-commit` within the `master branch`.

```
#!/bin/sh
git checkout gh-pages
git checkout master rmarkdown-syntax-highlighting.html
git rm -f index.html
git mv rmarkdown-syntax-highlighting.html index.html
git add .
git commit -m "$(git log -1 master --pretty=%B)"
git checkout master
```

Whenever I commit to the `master` branch, the same commit is also commited to the `gh-pages` branch.  This could have been accomplished using a `git merge` or a `git rebase` but that would necessitate the files having the same names and would potentially add other artifacts (\*.md or \*.Rmd) to the `gh-pages` branch.  Instead, this preserves the name `index.html` in the `gh-pages` branch.

Finally, in order to `git push` to both the `origin/master` and `origin/gh-pages` branches, I updated the `.git/config` file to include the following.

```
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
[remote "origin"]
    url = https://github.com/curtisalexander/rmarkdown-syntax-highlighting.git
    fetch = +refs/heads/*:refs/remotes/origin/*
    push = +refs/heads/master:refs/heads/master
    push = +refs/heads/gh-pages:refs/heads/gh-pages
[branch "master"]
    remote = origin
    merge = refs/heads/master
[branch "gh-pages"]
    remote = origin
    merge = refs/heads/gh-pages
```
