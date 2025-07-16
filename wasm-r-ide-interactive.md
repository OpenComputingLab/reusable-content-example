# WASM-R interactive

Can we run R interactively in the browser from a file, displaying any graphical input that is generated as well as text output and console messages?

The [`webR` REPL app](https://webr.r-wasm.org/latest/) is a demo application that follows a standard IDE layout to achieve just this.

```{figure} images/webR-repl.png
:name: webr_repl_preview
:width: 600px

Screenshot or WebR REPL.

A four panel layout is shown: top left is a file editor with a named file, and file save and run buttons; botton left is a text output area and concole; top right is a file browser with options to create and delete files, upload and download files; and bottom right is a graphical display area. A sinple program to generate a ggplot chart is shown in the top left code editor, and the corresponding ggplot chart output in the bottom right graphical display area.
```

To insert the `webR` REPL app into a VLE page, all we need to do is add the following invocation to our markdown:

````text
```{ou-html5} resources/webr-repl-01.zip
:width: 140
:keep: always
```
````

```{ou-html5} resources/webr-repl-01.zip
:width: 140
:keep: always
```

*The `:keep:` parameter uses the provided filename in the vendored files, rather than assigning a filename.*

ISSUES:

- whilst files can be saved during a session, they do not appear to be saved to browser storage?
- the form factor is not ideal...:
  - is there a way to launch the iframe as full screen view?
  - It would be useful if the REPL could be detached from the page and "popped out" into its own floating, resizable widget.
  - Alternatively, we could use a level of separation and just link to a REPL environment on separate URL and launch it in a new window, then encourage students to work with it side by side with the VLE instructional material window;
- a simpler view with just an a file edit window, console and graphical display might be more convenient.
