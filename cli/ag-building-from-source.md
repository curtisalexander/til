# `ag` - Building From Source

Building [the silver searcher](https://github.com/ggreer/the_silver_searcher) from source.

```
export PCRE_LIBS="-L/usr/lib -lpcre"
export PCRE_CFLAGS=-I/usr/include/pcre

./build.sh
sudo make install
```
