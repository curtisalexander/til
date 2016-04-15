# Transpose a List

[Kevin Ushey](https://github.com/kevinushey) tweeted this gem.  To transpose a list in R.

```r
transpose <- function(list) do.call(Map, c(c, list))
```
