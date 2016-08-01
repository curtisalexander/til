# Spark Version

Drop into `spark-shell`.  Requires that `kinit` has been run to generate a Kerberos ticket.

```bash
spark-shell
```

Once in the `spark-shell`, execute the following.

```bash
scala> sc.version
```

This is the version that needs to be set for the environment variable `SPARK_HOME_VERSION` when utilizing [sparklyr](http://spark.rstudio.com)
