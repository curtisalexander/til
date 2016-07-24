# Sparse Clone

What if I only want to `git clone` a subdirectory from [github](https://github.com)?

The example below clones just the `iterm2` color schemes from [junegunn/seoul256.vim](https://github.com/junegunn/seoul256.vim)

```sh
# create an empty repo with my remote, fetching all objects but
#   not checking them out
mkdir -p ~/code/seoul256.vim
cd ~/code/seoul256.vim
git init
git remote add -f origin https://github.com/junegunn/seoul256.vim

# sparse clone
git config core.sparseCheckout true

# define files and folder to checkout
echo "iterm2" >> .git/info/sparse-checkout

# update empty repo
git pull origin master

# alternatively perform a shallow clone cutting off history
# git pull --depth=1 origin master
```

From the [stackexchange] answer by [muru](http://unix.stackexchange.com/a/233335).
