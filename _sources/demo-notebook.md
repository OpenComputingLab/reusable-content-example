# Example publishing from Jupyter notebook

As well as authoring content in MyST markdown files, we can also author content in Jupyter notebooks.

As might be expected, notebook markdown cells support the full range of simple markdown syntax elements such as *emphasised* and __bold font__ content, as well as lists:

- item 1
- item 2

and quotes:

> My quotation

But we can also use notebooks to generate output content from code.

For example, we can create a simple data table:


```python
import pandas as pd

df = pd.DataFrame({"x": [1, 2, 3], "y":[10,3, 7]})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



And then generate a simple plot from the data:


```python
df.plot(x="x", y="y").set_title("My plot");
```
    
![png](demo-notebook_files/demo-notebook_3_0.png)
    

An output chart image is created directly from the data in the dataframe.

The image is saved to an image file and then embedded back into the generated HTML in the Jupyter Book HTML publishing processing, but currently the XML generation process does not generate the image file or reference it via a tag in the XML.

Related discussion: https://github.com/orgs/executablebooks/discussions/1096
