# Markdown authoring route

The reusable content workflow is based on a markdown authoring route.

Markdown is a simple text based markup language that can be edited in simple text editor. Markdown is typically rendered or previewed as rendered HTML. Markdown editors that support WYSIWYG user interfaces are also available. Various flavours of markdown are available that extend the core markdown language with more expressive semantics.

A variety of publishing tools and frameworks are available that can render markdown source documents to a wide range of output document formats, including HTML, PDF, ebook and XML formats.

As well as rendering rich text, markdown publishing extensions can also be used to render diagrams. For example, flowcharts can be rendered from simple text-based `Mermaid.js` scripts.

```{mermaid}
:alt: 
:caption: Publishing workflows from MyST markdown

flowchart LR
  A[Jupyter Notebook] --> C
  B[MyST Markdown] --> C
  C(mystmd) --> D{"Sphinx\n+\npandoc"}
  D --> E[LaTeX]
  E --> F[PDF]
  D --> G[Word]
  D --> H[XML] --> I[OU-XML]
  D --> J[HTML]
  I --> K[OU-VLE]
  I --> L[OU-PDF]
```

Example publishing tools and frameworks for working with markdown include:

- [`pandoc`](https://pandoc.org/): a low level computation tool for converting between different document formats;

- [Sphinx](https://www.sphinx-doc.org/en/master/): originally developed to support the publication of software documentation, but is now widely used for more general forms of publishing;

- [Jupyter Book](https://jupyterbook.org/en/stable/intro.html): publishing system built on top of Sphinx that supports the publication of content generated in whole or part from computational documents, (documents that include executable code whose outputs maybe be included in the output document); source documents include markdown and Jupyter notebooks; uses MyST flavoured markdown.

- [Quarto](https://quarto.org/docs/authoring/markdown-basics.html): scientific document publishing system; source documents include markdown as well as computational documents such as Jupyter notebooks and Quarto flavoured  markdown (`.qmd`).

````{admonition} MyST markdown sandbox

You can try out the MyST markdown sandbox editor [here](https://mystmd.org/sandbox).

```{figure} images/myst_preview.png
:name: myst_preview
:alt: screenshot of MyST sandbox editor
:width: 600px

Screenshot of MyST sandbox editor with live preview.
```

````

See TO DO  for guidance on how to launch a preconfigured development environment within which you can try out the workflow described in this document.

## OU-XML production workflow using Jupyter Book

An increasing number of OU modules that require students to work with executable computer code are starting to use Jupyter notebooks to provide students with an interactive learning environment that blends rich content with embedded executable code and rendered code outputs ({numref}`notebook_preview`).

```{figure} images/notebook_preview.png
:name: notebook_preview
:alt: screenshot of Juoyer notebook
:width: 600px

Screenshot of Jupyter notebook.
```

To support as general a workflow as a possible, the workflow adopted builds on the Jupyter Book publishing system. This supports:

- rich markdown (MyST syntax);
- markdown and/or Jupyter notebook source documents;
- executable content (via `jupyter-server`);
- conversion to OU-XML via `ou-book-theme`.

The workflow proceeds as follows:

- source content authored in one or more markdown files; a tables of contents file (`_toc.yml`) identifies the source files and the orfer in which they are presented;
- source content converted to output formats including Sphinx-XML by Sphinx;
- Sphinx-XML converted to OU-XML.

### Defining the table of contents (`_toc.yml`)

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

If no file suffix is provided for the filename, the build process will look for files with the markdon (`.md`) or Jupyter notebook (`.ipynb`) file suffix.

Typically, each file will define a single `<Session>` in the corresponding `<Item>`. Each file should start with a level 1 heading; lower level headings within each file trigger the creation of an `<InternalSection>` at that point. The  `<InternalSection>` blocks may be nested in line with ever subordinate heading levels.

Internal `<CrossRef>` links may be generated within each part by referencing the file name and an identifier derived the linked to (sub)heading. 