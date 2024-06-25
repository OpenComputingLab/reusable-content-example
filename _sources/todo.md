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

# Work in Progress

Examples of markdown markup that hasn't yet been mapped over to corresponding OU-XML tags...

## Glossary Items

We can define a glossary term as:

````text
```{glossary}
Glossary term one
  Glossary term one definition is indented
```
````

```{glossary}
Glossary term one
  Glossary term one definition is indented
```

We can then refer to a ``{term}`Glossary term one` TO DO`` that links to the glossary listing.

```{glossary}
A Glossary term two
  Glossary term two definition is indented
  No blank line

  Blank line

Glossary term three
  Glossary term three defintion
```

## YouTube Video items (sphinx-contrib.youtube)

We can embed video items as:

````text
```{youtube} PmxZywVwhP8
```
````

```{youtube} PmxZywVwhP8
Some text
```

## Code Execution

We should be able to execute code purely within the browser using `thebe`.

We should also be able to execute code as part of a Sphinx publishing process. Currently, rich media code outputs will be rendered in the HTML output, but only simple `text_plain` outputs are rendered into the Sphinx XML and then literally into OU-XML.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import pandas as pd

np.random.seed(24)
df = pd.DataFrame({'A': np.linspace(1, 10, 10)})
df = pd.concat([df, pd.DataFrame(np.random.randn(10, 4), columns=list('BCDE'))],
               axis=1)
df.iloc[3, 3] = np.nan
df.iloc[0, 2] = np.nan

def color_negative_red(val):
    """
    Takes a scalar and returns a string with
    the css property `'color: red'` for negative
    strings, black otherwise.
    """
    color = 'red' if val < 0 else 'black'
    return 'color: %s' % color

def highlight_max(s):
    '''
    highlight the maximum in a Series yellow.
    '''
    is_max = s == s.max()
    return ['background-color: yellow' if v else '' for v in is_max]

df.style.\
    applymap(color_negative_red).\
    apply(highlight_max).\
    set_table_attributes('style="font-size: 10px"')
```
