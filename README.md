Sequence and Graph diagrams in your markdown files!
=========================

> ## Solves the issue with missing arrow-heads in macOS + pandoc 1.19.2.1
> **The fix** => This forked version uses `mermaid@7.0.0`.
<br>

`mermaid-filter` is a pandoc filter that adds support for [mermaid](http://knsv.github.io/mermaid/) syntax diagrams in markdown.

Write your diagrams in fenced code blocks as usual like this:

```````markdown
\~~~mermaid
sequenceDiagram
    Alice->>John: Hello John, how are you?
    John-->>Alice: Great!
\~~~
```````

and get this in rendered doc ![rendered](https://cdn.rawgit.com/raghur/mermaid-filter/master/img/diagram-1.svg)

Installation and usage
---------------------

3. `npm install --global raghur/mermaid-filter`

`pandoc -t html -F mermaid-filter -o something.html something.md`

**WINDOWS** - you need `mermaid-filter.cmd` in the line above

**Windows 8.1** - On windows 8.1, `mermaid-filter.cmd` fails - apparently due to change in how the CMD.exe works
for subprocesses? - see this [issue thread](https://github.com/jgm/pandoc/issues/3458).
You have to edit the globally installed `mermaid-filter.cmd` located in `c:\users\<username>\AppData\Roaming\npm`
to use `~dp$PATH:0`.
Unfortunately, you will need to do this each time you install/update mermaid-filter since it overwrites the cmd file.

Options
--------------------

You have a couple of formatting options via attributes of the fenced code block to control the rendering

- Image Format - Use \`\`\`{.mermaid format=svg}     Default is png
- Width  - Use \`\`\`{.mermaid width=400}     default with is 500
- Save path - Use \`\`\`{.mermaid loc=img}  default loc=inline which will
  encode the image in a `data uri` scheme.
    - Possible values for `loc`
        - `loc=inline` - default; encode image to data uri on img tag.
            - For widest compatibility, use png (default)
            - SVG has trouble on IE11
        - `loc=imgur` - upload png to imgur and link to it.
        - `loc=<anythingelse>` -treat as folder name to place images into

Note that to specify options, you need to use the curly braces syntax and have the `.mermaid` class attached.
Admittedly, this is uglier than the earlier syntax on top - but that's how Pandoc wants it.
