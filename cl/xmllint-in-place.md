# Format an XML In-Place
In order to format an XML in place -- reading the XML in, formatting, and then writing back out with the same name, execute the following.

```bash
xmllint -o tst.xml --format tst.xml
```

Thanks to Daniel Veillard at https://mail.gnome.org/archives/xml/2010-August/msg00005.html.
