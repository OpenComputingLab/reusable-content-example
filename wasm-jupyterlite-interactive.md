# JupyterLite interactive coding

JupyterLite provides an in-browser JupyterLab environment capable of executing code within the browser using WASM based code execution environments for JavaScript, Python and R.

```{ou-html5} resources/jupyterlite-01.zip
:width: 140
:keep: always
```

This doesn't quite work yet; if we hack the iframe source and change the path `index.html` to `lab/indexhtml` it will work (although currently there are no code execution kernels installed).)

![](images/jupyterlite_moodle.png)

JupyterLite also supports a notebook view and a console. which opens up various interesting possibilities. There is also an extension that allows files to be opened into JupyterLab from the desktop when using the Chrome browser, although this extension is not currently installed.

## How do we make the JupyterLite zip file?

Create a jupyerlite site and zip it?

```bash
cd dist/
zip -r ../jupyterlite-dist.zip .
```
