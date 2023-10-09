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

```python
# A comment
def demo():
    """An example function.
    """
    a = 1
    return a

demo()
```

*In Markdown, the backticked block typically also defines the language so that languge sensitive syntax highlighting can be applied appropriately.*

This renders to OU-XML as:

```xml
<ProgramListing>
  <Paragraph># A comment</Paragraph>
  <Paragraph>def demo():</Paragraph>
  <Paragraph>    """An example function.</Paragraph>
  <Paragraph>    """</Paragraph>
  <Paragraph>    a = 1</Paragraph>
  <Paragraph>    return a</Paragraph>
  <Paragraph></Paragraph>
  <Paragraph>demo()</Paragraph>
</ProgramListing>
```

We can also refer inline, for example to the `pandas` package.

This renders to OU-XML as:

```xml
<Paragraph>We can also refer inline, for example to the <ComputerCode>pandas</ComputerCode> package.</Paragraph>
```