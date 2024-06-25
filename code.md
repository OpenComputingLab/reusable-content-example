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

# Code

We can mark up code blocks in usual markdown style by using a triple backticked block to delimit the code block:

````text
```python
# A comment
def demo():
    """An example function.
    """
    a = 1
    return a

demo()
```
````

*In Markdown, the backticked block typically also defines the language so that language sensitive syntax highlighting can be applied appropriately.*

If we set `ou.codestyle: true` in the `_config.yml` file, we style the code block using the centrally maintained [`codesnippet` HTML widget](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2235581).

```python
# A comment
def demo():
    """An example function.
    """
    a = 1
    return a

demo()
```

*We can also set the theme from the `_config.yml` file (`codesnippet_theme: light | dark `).*

The unstyled "rendered" code is described in OU-XML as:

```xml
<Paragraph>
  <br/>
  # A comment<br/>
  def demo():<br/>
  """An example function.<br/>
  """<br/>
  a = 1<br/>
  return a<br/>
  <br/>
  demo()
</Paragraph>
```

*Note that OU-XML does not support the declaration of the language type, which makes roundtripping support for language sensitive syntax highlighting difficult.*

We can also refer to code inline, for example to the `pandas` package.

This renders to OU-XML using the `<ComputerCode>` tag:

```xml
<Paragraph>We can also refer inline, for example to the <ComputerCode>pandas</ComputerCode> package.</Paragraph>
```

## Styled code

If we don't want to style all the code blocks automatically, we can manually apply style using `prism.js` to particular blocks via the `{ou-codestyle}` admonition block:

```{ou-codestyle} python
# some code

def test():
  """A function."""
  print("hello")
```

Pass the language name in to define the language pack styling.

TO DO - add themes?

## Code execution workflow — NOTES — TO DO

The conversion over things like rendered Jupyter notebooks to Sphinx XML seems to introduce clutter and miss certain outputs compared to how Jupyter Book HTML cleanly renders cell outputs for example. Which means no quick wins churning the Sphinx XML to OU-XML as a way of getting code rendered assets into OU-XML.

However, I think there is a multi-step pathway that works:

- convert md and ipynb files to ipynb using jupytext
- use nbconvert to execute notebooks and render them to markdown; this markdown seems to include code outputs in a reasonably sensible way - eg we get image links and image files out.
- use the markdown as the basis for the conversion to OU=XML

So I'm thinking of a directory structure such as:

```text
_toc.yml
_config.yml
src/
  - example.md
  - example2.ipynb
intermediate/
  # generated via jupytext
  - example.ipynb
  - example2.ipynb
executed/
  # generated via nbconvert
  - example.md
  - example2.md
```

The same top-level `_toc.yml` file should be useable against each directory if we need to use it, even if we manually have to copy it in to the content directories and run tools directly within those directories etc.
