# TeXmacs markdown plugin

This plugin is a (for now one-way) converter to markdown format for 
[TeXmacs](http://www.texmacs.org/). It supports most of the standard Markdown 
syntax, plus much of TeXmacs' non-dynamic markup. In particular, labels and 
references, numbered environments and figures should work out of the box. The 
major exception is tables, but this can be overcome by exporting them to html 
and pasting into the markdown file.

The plugin has been developed for its use in two specific websites, 
[Paperwhy](https://paperwhy.8027.org/) and appliedAI's 
[TransferLab](https://transferlab.appliedai.de/), and can use multiple 
extensions specific to the static website generator [Hugo](https://gohugo.io/). 
There might still be some code very specific to those sites, YMMV.

## Setup

Clone this repository into your `~/.TeXmacs/plugins` directory as `markdown`. 
For Linux / OSX this is:

```shell
git clone https://bitbucket.org/mdbenito/tm2md.git ~/.TeXmacs/plugins/markdown
```


For Windows, the path (usually?) is

```shell
\Users\YourUser\AppData\Roaming\TeXmacs\plugins
```


You can activate a menu with Tools -> Markdown plugin.

## Hugo support

In addition to standard markdown, almost everything that Hugo supports can be 
converted from TeXmacs, including setting frontmatter values and extensions 
like footnotes and ~~striked through text~~.

Setting values for the frontmatter is suported via a dedicated macro defined 
in `hugo.ts`. To use it first insert the Markdown -> Hugo package in Document 
-> Style -> Add package or using plus sign in the focus bar.

Now you can type `\hugo-front` and input any number of key|value pairs as 
arguments, one argument each. That is: type `\hugo-front`, then use structured 
insert right to add two arguments and use the first for the key and the second 
for the value. Repeat as needed. Currently, only strings, lists of strings and 
dates (insert with `\date`) are supported as values. To enter a list, input 
`\tuple` as the value and use structured insert right to add items.

### Supported shortcodes

  * Figures are converted to `{{< figure … >}}`
  * For arbitrary shortcodes, use `\hugo-short`.
  * Citations are automatically detected and converted to `{{< cite ref >}}`, 
  and all of them are gathered in the frontmatter as well, for indization by 
  Hugo's taxonomy system.
  * Probably more…

# Known issues

  * The converter can break with malformed or unexpected input, like markup 
  inside tags whose values should be strings (although many cases are 
  “handled”)
  * Error reporting is rather lacking. Run TeXmacs in a console to see stack 
  traces and such in case you are running into problems.
  * No tables (yet)!
  * Images must be linked, not embedded in the document.

# To do

  * Reverse markdown to TeXmacs conversion.
  * Declare converter options in init file, and use.
  * Extract all Hugo extensions to a separate file, use overloading and 
  extension of the dispatch hashmaps.
  * Use “converter environments”?
  * Use TeXmacs' `logic-dispatch`?
  * line-breaks and other markup in doc-data (e.g. in the doc-title) need to be 
  properly handled if included in YAML metadata for Hugo.
  * Support for tables.
  * Extract embedded images.

# License

[GPL v3](https://www.gnu.org/licenses/gpl-3.0.en.html).