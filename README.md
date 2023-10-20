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



+++

+++

# reusable-content-example

Informal report on creating reusable / generic content as Markdown text with conversion to OU-XML

## Build process

Generate the Sphinx XML version of the Jupyter Book, as defined by the `_toc.yml` and `_config.yml` file:

`jb build . --builder custom --custom-builder xml`

Convert to OU-XML:

`obt convert-to-ouxml .`

Initialise documents:

- if only one hernel is available, it will be specified in inital metadata: `jupyter-book myst init *.md`
- if multiple jernels are available (they will be listed when you run the above comment), you must spoecify which kernel to use; for example: `jupyter-book myst init *.md --kernel python3`

Convert to MyST md:

`jupytext --to myst *.md`

## `.devcontainer` Set-up

The `.devcontainer` set up allows you to run the build tools ... TO DO

## Spellchecking and formatting

Using [`tbroadley/spellchecker-cli`](https://github.com/tbroadley/spellchecker-cli):

`spellchecker --files  *.md --language en-GB --dictionaries rce-dictionary.txt`

Formatting using [`mdformat`](<>):

`mdformat .`
