# Markdown Within Outlook
The below will allow one to write an email within Outlook using Markdown.  Or one can copy Markdown directly into a message body and convert it inplace.

The key to this conversion is utilizing the [Markdown Service Tools](http://brettterpstra.com/projects/markdown-service-tools/) created by Brett Terpstra.

## Setup
* Install `multimarkdown`

```sh
brew install multimarkdown
```

* Download and install Brett's [Markdown Service Tools](http://brettterpstra.com/projects/markdown-service-tools/).  Once downloaded, install by double-clicking on the `automator` workflow.

## Usage

Write your email in Outlook using Markdown. When ready to convert, highlight the Markdown text and select `md - Convert - MultiMarkdown to RTF` from the `Services` menu.  This will replace the Markdown inline as RTF.
