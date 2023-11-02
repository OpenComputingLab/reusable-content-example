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

# Markdown authoring route

The reusable content workflow is based on a markdown authoring route. Content is authored in markdown format and then converted to the intermediate OU-XML format, or directly to output formats such as HTML. Content in the OU-XML format can be rendered to the VLE or other output formats using the current Structured Content production workflow tools.

Markdown is a simple text based markup language that can be edited in simple text editor. Markdown is typically rendered or previewed as rendered HTML. Markdown editors that support WYSIWYG user interfaces are also available. Various flavours of markdown are available that extend the core markdown language with more expressive semantics.

A variety of publishing tools and frameworks are available that can render markdown source documents to a wide range of output document formats, including HTML, PDF, ebook and XML formats.

As well as rendering rich text, markdown publishing extensions can also be used to render diagrams. For example, flowcharts can be rendered from simple text-based `Mermaid.js` scripts.

```{mermaid}
---
alt:
caption: Publishing workflows from MyST markdown
---
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

*The flowchart above was automatically rendered and embedded from a `mermaid.js` admonition block in the source markdown document.*

````text
```{mermaid}
---
alt:
caption: Publishing workflows from MyST markdown
---
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
````

## Example markdown styling

Simple markdown styling supports the rendering of *emphasis* and __strong__ elements through simple markup.

The raw markdown has the form:

```text
Simple markdown styling supports the rendering of *emphasis* and __strong__ elements through simple markup.
```

In the mapping to OU-XML, the original markdown would be converted to:

```xml
 <Paragraph>Simple markdown styling supports the rendering of <i>emphasis</i> and <b>strong</b> elements through simple markup.</Paragraph>
```

Simple lists can also be defined. For example, unordered lists:

- item one
- item two

are written in markdown as:

```text
- item one
- item two
```

An unordered list is rendered to OU-XML as:

```xml
<BulletedList>
  <ListItem>
    <Paragraph>item one</Paragraph>
  </ListItem>
  <ListItem>
    <Paragraph>item two</Paragraph>
  </ListItem>
</BulletedList>
```

Ordered lists are also supported:

1. item one
1. item two

The source of ordered lists just needs to identifying numbering should be used; the actual numbers are generated:

```text
1. item one
1. item two
```

An ordered list is then rendered into OU-XML as:

```xml
<Paragraph>as well as ordered lists:</Paragraph>
<NumberedList>
  <ListItem>
    <Paragraph>item one</Paragraph>
  </ListItem>
  <ListItem>
    <Paragraph>item two</Paragraph>
  </ListItem>
</NumberedList>
```

Simple tables can be described using the markdown table format. The markdown table format supports alignment within columns but the alignment does not carry over to the OU-XML:

```text
| Col 1 | Col 2         | Col 3  |
|-------|:-------------:|-------:|
| col 1 |  left-aligned | L      |
| col 2 |    centered   | center |
| col 2 | right-aligned | R      |

```

| Col 1 |     Col 2     |  Col 3 |
| ----- | :-----------: | -----: |
| col 1 | left-aligned  |      L |
| col 2 |   centered    | center |
| col 2 | right-aligned |      R |

Here's fragment of the corresponding OU-XML:

```xml
<Table>
  <TableHead>Table 1 </TableHead><tbody>
    <tr>
      <th class="ColumnHeadLeft">
          <Paragraph>Col 1</Paragraph>
      </th>
      <th class="ColumnHeadLeft">
          <Paragraph>Col 2</Paragraph>
      </th>
      <th class="ColumnHeadLeft">
          <Paragraph>Col 3</Paragraph>
      </th>
    </tr>
    <tr>
      <td>
        <Paragraph>col 1</Paragraph>
      </td>
      <td>
        <Paragraph>left-aligned</Paragraph>
      </td>
      <td>
        <Paragraph>L</Paragraph>
      </td>
    </tr>
    <tr>
      <td>
        <Paragraph>col 2</Paragraph>
      </td>
      <td>
        <Paragraph>centered</Paragraph>
      </td>
      <td>
        <Paragraph>center</Paragraph>
      </td>
    </tr>
  </tbody>
</Table>
```

Boxes can be defined using MyST markdown admonition blocks:

````text
```{admonition} Box Title

Here is the box content.

It can contain a *wide* __range__ of elements.
```
````

```{admonition} Box Title

Here is the box content.

It can contain a *wide* __range__ of elements.
```

```xml
  <Box>
    <Heading>Box Title</Heading>
    <Paragraph>Here is the box content.</Paragraph>
    <Paragraph>It can contain a <i>wide</i> <b>range</b> of elements.</Paragraph>
  </Box>
```

A wide range of richer media elements are also supported by MyST markdown and can be mapped onto appropriate OU-XML elements (see later sections for examples).

## Markdown Publishing Tools and Frameworks

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

*I hope to make a `sandbox` available at some point in the near future, in the form of guidance on how to launch a preconfigured development environment within which you can try out the workflow described in this document.*
