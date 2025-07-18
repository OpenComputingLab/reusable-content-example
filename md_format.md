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

# Markdown format

The MyST markdown format supports a range of mark-up devices that can be mapped naturally onto OU-XML tags. The format can also be extended to support the parsing, rendering and conversion of additional, custom defined tags.

## From markdown to OU-XML

The range of MyST markdown elements that currently map on to OU-XML tags include:

### Headings

Use standard markdown heading levels (one or more `#` characters at start a line, followed by whitespace and then the header. The number of `#` characters specifies the heading level).

Each included file represents a session and should start with a first level heading. Interior headings within the file (second level, third level, etc.) are associated with increasingly nested `<InternalSection>` tags, with the heading mapped to the `<Title>` tag at the start of the section.

If the `sphinx.config.myst_heading_anchors` is set in the `_config.yml` file, identifiers are associated with each `<Session>` and `<InternalSection>` to the specified depth based on decasing the heading, removing punctuation and replace spaces with a `-`. Any generated section or subsection numbering is ignored.

For example, `## Second level heading` would map to:

```text
<Session id="introduction">
    <Title>1 Introduction</Title>
    ...
    <InternalSection id="second-level-heading">
        <Heading>Second level heading</Heading>
    ...
```

Note that section headings need to be unique within a `<Session>` if they are to be resolved as cross-referenced sections.

### Cross-references

Cross-references may be made to section or internal section headers in the same file / session, or to other files / sessions in the same item by means of the session or internal section identifier.

### Figure elements

Figure elements should be defined in markdown as follows:

````text

```{figure} assets_path/images_path/image_file.png
:name: unique_image_reference

Caption text

Optional description text for the image. Possibly several sentences.

```
````

This then maps onto the following OU-XML:

```xml
<Figure>
    <Image src="https://generated.url/path/image_file.png"/>
    <Caption>Figure N.M Caption text</Caption>
    <Description>
        <Paragraph>Optional description text for the image. Possibly several sentences.</Paragraph>
    </Description>
</Figure>
```

Several settings in the `_config.txt` determine how references to the figure are generated:

```yaml
sphinx:
    config:
        numfig: true
        numfig_format: {'figure':'Figure %s'}
        numfig_secnum_depth: 1 #eg 0:1 1:2.1
```

The `numfig` parameter determines whether numeric references to figures may be generated; the `numfig_format` parameter specifies the format of the numeric reference text when a reference is generate; and the `numfig_secnum_depth` identifies the numbering level (incremental figure count across the item (`0`) or section number and figure number within section (`1`)).

Links to figures can be described in the text via the unique reference, and either the caption text (`` {ref}`unique_image_reference`) ``) or, if enabled, the generated numeric reference (`` {numref}`g-other_file_in_item.md#unique_image_reference`  ``) may be displayed.

If the reference is to a figure in a separate file, the path to the source filename should also be specified (for example, `` {numref}`unique_image_reference`  `` or `` {ref}`other_file_in_item.md#unique_image_reference`  ``).

An optional `_config.yml` configuration setting, `ou.image_path_prefix`, allows a path to the image directory to be specified.

```yaml
ou:
  image_path_prefix: https://generated.url/path
  # For example:
  # image_path_prefix: https://openuniv.sharepoint.com/sites/mmodules/m348/lmimages/
 
```

### Component numbering

Automatic numbering may be enabled via the `_toc.yml` file.

## Extending the markup language

The MyST markdown format and the Sphinx publishing framework are both extensible, which means that it is possible to define additional tags to support the creation of bespoke materials.

For example, the publishing workflow has been extended to include support for:

- the parsing and rendering of `mermaid.js` diagram syntax;
- the parsing and custom rendering of "activities" with revealable answers;
- the embedding of video, audio, and zipped HTML5 assets

Appropriate conversions take place when a markdown document is converted toi OU-XML. In addition, OU-XML documents can be converted back to appropriately structured markdown documents.
