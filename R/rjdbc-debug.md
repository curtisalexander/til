# Debugging RJDBC

When using `RJDBC` within `R`, errors of the form

```
Error in .jfindClass(as.character(driverClass)[1]) : class not found
```

are a potential misnomer.  In order to actually debug the issue, execute the following

```r
.jclassLoader()$setDebug(1L)
```
