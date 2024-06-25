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

# OU-XML production workflow using Jupyter Book

An increasing number of OU modules that require students to work with executable computer code are starting to use Jupyter notebooks to provide students with an interactive learning environment that blends rich content with embedded executable code and rendered code outputs ({numref}`notebook_preview`).

```{figure} images/notebook_preview.png
---
name: notebook_preview
alt: screenshot of Juoyer notebook
width: 600px
---
Screenshot of Jupyter notebook.
```

To support as general a workflow as a possible, the workflow adopted builds on the Jupyter Book publishing system. This supports:

- rich markdown (MyST syntax);
- markdown and/or Jupyter notebook source documents;
- executable content (via `jupyter-server`);
- conversion to OU-XML via `ou-book-theme`.

The workflow proceeds as follows:

- source content authored in one or more markdown files; a tables of contents file (`_toc.yml`) identifies the source files and the order in which they are presented;
- source content converted to output formats including Sphinx-XML by Sphinx;
- Sphinx-XML converted to OU-XML.

## Defining the table of contents (`_toc.yml`)

The table of contents file can be used to define the contents of one of more OU-XML documents, where each part in the `_toc.yml` file defines a structured content `<Item>`.

```yaml
format: jb-book
root: _copyright_notice
parts:
  - caption: First item name
    numbered: true
    chapters:
      - file: introduction
      - file: first_section
      - file: another_section
      - file: conclusion
  - caption: Second item name
    numbered: true
    chapters:
      - file: introduction2
      - file: only_section
      - file: conclusion2
```

If no file suffix is provided for the filename, the build process will look for files with the markdown (`.md`) or Jupyter notebook (`.ipynb`) file suffix.

Typically, each file will define a single `<Session>` in the corresponding `<Item>`. Each file should start with a level 1 heading; lower level headings within each file trigger the creation of an `<InternalSection>` at that point. The  `<InternalSection>` blocks may be nested in line with ever subordinate heading levels.

Internal `<CrossRef>` links may be generated within each part by referencing the file name and an identifier derived the linked to (sub)heading.

## Build process

The build process for generating OU-XML from markdown is a two step process.

The first step is to use Jupyter Book tooling to generate a Sphinx XML version of the Jupyter Book, as defined by the `_toc.yml` and `_config.yml` files:

`jb build . --builder custom --custom-builder xml`

This generates XML files in the default `_build/xml` directory.

The second step is to use `ouseful_obt` from [`ou-xml-validator` package](https://github.com/innovationOUtside/ou-xml-validator/):

`ouseful_obt .`

Generated OU-XML content in the `_build/ouxml` directory can then be validated against an OU-XML schema by running the command:

`ou_xml_validator validate  path/to/testme.xml`
