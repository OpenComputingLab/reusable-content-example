
# OU-XML production workflow using Jupyter Book

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

The second step is to use the [`ou-book-theme`](https://pypi.org/project/ou-book-theme/) Python package to convert the Sphinx XML to OU-XML (this looks for XML source documents in `_build/xml` by default):

`obt convert-to-ouxml .`

*NB I think release version of `ou-book-theme` is laggiong the modified version I have been working on...*

Generated OU-XML content in the `_build/ouxml` directory can then be validated against an OU-XML schema by running the command:

`ou_xml_validator validate  path/to/testme.xml`

## Workflow Automation

A GitHub Action associated with this repository can be used to automatically:

- build and publish ah HTML version of this book from the source markdown (HTML book available [here](https://opencomputinglab.github.io/reusable-content-example/preface.html))
- build and publish the OU-XML from the source markdown (OU-XML document available [here](https://opencomputinglab.github.io/reusable-content-example//ouxmlxxx_b0_p1_zzz.xml) ; a zip archive file of the OU-XML and associated media asstets is ailable as an automatically generated GitHUb Action artefact attached to the `deploy-book` action reports [here](https://github.com/OpenComputingLab/reusable-content-example/actions/workflows/deploy-book.yaml) )

### Example GitHub Action automation script

```yaml
name: deploy-book

on:
  release:
    types: [published]
  workflow_dispatch:

# This job installs dependencies, builds the book, and pushes it to `gh-pages`
jobs:
  deploy-book:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    # Install dependencies
    - name: Set up Python 3.11
      uses: actions/setup-python@v1
      with:
        python-version: 3.11

    - name: Install dependencies
      run: |
        pip install jupyter-book ou-jupyter-book-tools
        pip install ou_book_theme sphinxcontrib.mermaid sphinxcontrib-youtube sphinx-exercise
    # Build the book
    - name: Build the book
      run: |
        jupyter-book build .
        touch ./_build/html/.nojekyll
    - uses: actions/setup-node@v3
      with:
        node-version: 18
    - name: Build the OU-XML
      run: |
        pip install https://github.com/innovationOUtside/ou-xml-validator/archive/refs/heads/main.zip
        jb build --builder custom --custom-builder xml .
        ouseful_obt .
        mkdir -p /var/tmp/dist
        cp -rf _build/ouxml /var/tmp/dist/
        cp -rf _build/ouxml ./_build/html
    # Push the book's HTML to github-pages
    - name: GitHub Pages action
      uses: peaceiris/actions-gh-pages@v3.6.1
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./_build/html
    - name: Upload docs bundle
      if: always()
      uses: actions/upload-artifact@v3
      with:
        name: ${{github.event.inputs.module}}_docs_bundle
        path: /var/tmp/dist
```