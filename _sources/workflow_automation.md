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
# Workflow Automation

A GitHub Action associated with this repository can be used to automatically:

- build and publish an HTML version of this book from the source markdown (HTML book available [here](https://opencomputinglab.github.io/reusable-content-example/preface.html))
- build and publish the OU-XML from the source markdown (OU-XML document available [here](https://opencomputinglab.github.io/reusable-content-example/ouxml/xxx_b0_p1_zzz.xml) ; a zip archive file of the OU-XML and associated media assets are available as an automatically generated GitHub Action artefact attached to the `deploy-book` action reports [here](https://github.com/OpenComputingLab/reusable-content-example/actions/workflows/deploy-book.yaml) )

## Example GitHub Action automation script

The following Github Action automation script is used to:

- checkout the contents of the repository;
- install requirements;
- build an HTML version of using Jupyter Book
- generate a Sphinx XML version;
- convert the Sphinx XML to OU-XML;
- publish the HTML version of the book to GitHub Pages;
- zip the OU-XML files and publish them as a workflow artifact in the GitHub Actions report for the job;

TO DO - valudate the generated OU-XML.

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
        pip install -r requirements.txt
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
