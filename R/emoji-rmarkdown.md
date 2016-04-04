# Emoji Within RMarkdown

To make use of emoji within RMarkdown, the yaml frontmatter of your RMarkdown document should include the `in_header` option.

```yaml
---
title: "My Title"
Author: "Curtis Alexander"
output: 
    html_document: 
        highlight: pygments
        self_contained: no
        theme: readable
        toc: yes
        toc_depth: 4
        toc_float: yes
        includes:
            in_header: header.md
runtime: shiny
---
```

Then within the `header.md` file, include the following which points to the [Twitter emoji library](http://twitter.github.io/twemoji/).

```
<script src="//twemoji.maxcdn.com/2/twemoji.min.js"></script>
```

Finally, to add an emoji it requires the Unicode value of the form

```
&#x1F416;
```

which is the emoji for a pig.  See the [Unicode Emoji Tables](http://apps.timwhitlock.info/emoji/tables/unicode) site for a good list of emoji and their corresponding Unicode values.
