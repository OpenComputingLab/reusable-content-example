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

*The mapping to appropriate XML tags is under development; currently it is only partially handled for `audio` items and not handled for `video` items.*

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

The MyST spec also lets you use a video file path in a `{figure}` admonition when generating HTML output, but this is not support for conversion to OU-XML.

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

## Visualising molecules

One of the attractions of this production route is that it can be quite straightforward to create simple markdown admonitions that can use third party Python packages to generate interactive HTML components, and then embed these in the resulting output documents.

he [`3dmol.js`](https://3dmol.csb.pitt.edu/) packages provides an interactive 3D viewer for a wide range of molecules.

We can create a simple Sphinx admonition handler that will accept a molecule query code (see the official docs for more info on this) and then render the molecule with desired styling.

We can then use a markdown admonition such as the following to generate an interactive widget that lets us interactively visualise the molecule:

````text
```{ou-mol3d} pdb:1ubq
:style: '{"sphere":{"radius":"0.5"}}'
```
````

to embed an interactive JavaScript powered viewer such as the following (click then drag in the widget below to rotate the rendered molecule; mouse/touchpad controls should also let you zoom in and out):

```{ou-mol3d} pdb:1ubq
:style: '{"sphere":{"radius":"0.5"}}'
:background: '0x222222'
```

*Note that the style information must be presented as a quoted string and take the form of a valid JSON string.*

*It would perhaps be usedul to try to follow the model of embedded audio and video players and also support captions, additional description text, etc. It may also make sense to automatically number this sort of embedded asset as a figure, or perhaps create an "Interactive Figure" type and associated numbering scheme?*
