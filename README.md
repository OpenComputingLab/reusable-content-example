---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.15.0
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# reusable-content-example

Informal report on creating reusable / generic content as Markdown text with conversion to OU-XML

## Quality Enhanced Build process

To improve the quality of output documents, we can use the a quality enhanced build process that includes markdown formatting and spellchecking prior to the generation of output formats and conversion to OU-XML.

### Spellchecking and formatting

Using [`tbroadley/spellchecker-cli`](https://github.com/tbroadley/spellchecker-cli):

`e--language en-GB --dictionaries rce-dictionary.txt`

Formatting using [`mdformat`](https://github.com/executablebooks/mdformat):

```bash
# pip3 install mdformat mdformat-myst
mdformat .
```

Additional custom cleaning of markdown files (useful following automated conversion of OU-XML to markdown):

`ou_xml_validator cleanmd PATH`

## Conversion to Jupytext / `MyST` executable markdown format

Initialise markdown documents as executable MyST markdown documents:

- if only one kernel is available, it will be specified in initial metadata: `jupyter-book myst init *.md`
- if multiple kernels are available (they will be listed when you run the above comment), you must specify which kernel to use; for example: `jupyter-book myst init *.md --kernel python3`

If no Jupytext header is required, convert to headerless MyST md:

`jupytext --to myst *.md`

If we have a notebook, execute and render to markdown:

`jupyter nbconvert --to markdown --execute demo-notebook.ipynb`

Then use the markdown format for conversion to OU-XML.

### Bundling HTML5.zip Packages

The HTML5.zip packages MUST include an `index.html` file at the root level.

### Generating Sphinx XML

Spell-checking:

`spellchecker --files  *.md --dictionaries rce-dictionary.txt  > spellingreport.txt`
`
Generate the Sphinx XML version of the Jupyter Book, as defined by the `_toc.yml` and `_config.yml` file:

`jb build . --builder custom --custom-builder xml`

In `jb build` use the `--all` to force a rebuild of everything.

### Convert to OU-XML

Convert to OU-XML (tool in `ou-xml-validator` package):

`ouseful_obt .`

We can then validate the OU-XML:

`ou_xml_validator validate path-to-file/testme.xml`

### JupyterLite

We need `index.html` at the root of an HTML5 zipfile; inside the `jupyterlite` dir: `zip -r -X "../jupyterlite.zip" .`

```bash
mkdir jupyterlite
cd jupyterlite
jupyter lite init 
cd _output  
jupyter lite build --output-dir ../../resources/jupyterlite-01
cd resources/jupyterlite-01
zip -r -X "../jupyterlite-01.zip" .
```

## `.devcontainer` Set-up

The `.devcontainer` set up allows you to run the build tools ... TO DO
