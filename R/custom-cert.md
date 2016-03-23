# Custom Certificate With `devtools`

In order to use `devtools::install_github()` with a custom certificate, perform the following.

Install `devtools`
```{r}
install.packages("devtools")
```

`devtools` makes use of `httr` for installations.  Thus, add the following to your `.Rprofile`
```
httr::set_config(httr::config(cainfo = 'C:/Users/calex/ca-bundle.crt'))
```
