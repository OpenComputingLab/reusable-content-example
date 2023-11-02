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

This is then rendered as a styled code block:

```python
# A comment
def demo():
    """An example function.
    """
    a = 1
    return a

demo()
```

This "rendered" block is described in OU-XML as:

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

*Note that there is no declaration of the language type to support language sensitive syntax highlighting.*

We can also refer to code inline, for example to the `pandas` package.

This renders to OU-XML using the `<ComputerCode>` tag:

```xml
<Paragraph>We can also refer inline, for example to the <ComputerCode>pandas</ComputerCode> package.</Paragraph>
```
