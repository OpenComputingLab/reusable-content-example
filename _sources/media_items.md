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

````text`
```{ou-video} resources/test.mp4
```
````

```{ou-video} resources/test.mp4
```

The MyST spec also lets you use a video file path in a `{figure}` admonition:

````text
```{figure} resources/test.mp4
My video caption

And description.

More description.
```
````

```{figure} resources/test.mp4
My video caption

And description.

More description.
```

...which is handy...

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

*Currently, there is no native MyST admonition for embedding an audio player.*
