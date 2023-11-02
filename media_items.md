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
# Embedded Media

Embedded media items can be specified in MyST markdown using custom `{video}` and `{audio}` admonitions and rendered into HTML using the [`innovationOUtside/sphinxcontrib-ou-xml-tags`](https://github.com/innovationOUtside/sphinxcontrib-ou-xml-tags) Sphinx extension.

*The mapping to appropriate XML tags is under developement; currently it is only partially handled for `audio` items and not handled for `video` items.*

## Video Items

Embedded video player using [`innovationOUtside/sphinxcontrib-ou-xml-tags`](https://github.com/innovationOUtside/sphinxcontrib-ou-xml-tags):

````text
```{ou-video} resources/test.mp4
A caption for a video file.

A line of description.
And continuation of the line.

More description.
```
````

```{ou-video} resources/test.mp4
A caption for a video file.

A line of description.
And continuation of the line.

More description.
```

The block can also be empty of caption and description text. *If there is any text in the body of the admonition, the first line is mapped onto an OU-XML `<Caption>` element.*

The MyST spec also lets you use a video file path in a `{figure}` admonition when geberating HTML output, but this is not support for conversion to OU-XML.

## Audio Items

Audio player using [`innovationOUtside/sphinxcontrib-ou-xml-tags`](https://github.com/innovationOUtside/sphinxcontrib-ou-xml-tags):

````text
```{ou-audio} resources/test.mp3
A caption for an audio file.
```
````

```{ou-audio} resources/test.mp3
A caption for an audio file.
```

As with the `ou-video` element, we can optionally include a caption, or a caption and description elements, by including text inside the admonition block.

*Currently, there is no native MyST admonition for embedding an audio player.*
