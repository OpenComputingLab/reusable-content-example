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

## Example Markdown Styling

Simple markdown styling supports the rendering of *emphasis* and __strong__ elements through simple markup.

These are rendered to OU-XML as:

```xml
 <Paragraph>Simple markdown styling supports the rendering of <i>emphasis</i> and <b>strong</b> elements through simple markup.</Paragraph>
```

Simple lists can also be defined. For example, unordered lists:

- item one
- item two

as well as ordered lists:

1. item one
1. item two

The unordered list is rendered to OU-XML as:

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

The following paragraph and the ordered list are then rendered as:

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

Simple tables can be described using the markdown table format. The table format supports alignment within columns but the alignment does not carry over to the OU-XML:

```text
| Col 1 | Col 2         | Col 3  |
|-------|:-------------:|-------:|
| col 1 |  left-aligned | L      |
| col 2 |    centered   | center |
| col 2 | right-aligned | R      |

```

| Col 1 | Col 2         | Col 3  |
|-------|:-------------:|-------:|
| col 1 |  left-aligned | L      |
| col 2 |    centered   | center |
| col 2 | right-aligned | R      |

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

See `sandobox` for guidance on how to launch a preconfigured development environment within which you can try out the workflow described in this document.
