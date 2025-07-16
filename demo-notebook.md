# Example publishing from Jupyter notebook

As well as authoring content in MyST markdown files, we can also author content in Jupyter notebooks.

As might be expected, notebook markdown cells support the full range of simple markdown syntax elements such as *emphasised* and __bold font__ content, as well as lists:

- item 1
- item 2

and quotes:

> My quotation

But we can also use notebooks to generate output content from code.


For example, generating print output from a cell:



```{code-cell} python

print("hello")
```

+++ {"tags": ["code-cell-output"]}

hello

+++

For example, we can create a simple data table:



```{code-cell} python

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




+++ {"tags": ['activity'] }

And then generate a simple plot from the data:

+++


```{code-cell} python
:tags: ['activity']
df.plot(x="x", y="y").set_title("My plot");
```


    
```{image} demo-notebook_files/demo-notebook_6_0.png
```



An output chart image is created directly from the data in the dataframe.

The image is saved to an image file and then embedded back into the generated HTML in the Jupyter Book HTML publishing processing, but currently the XML generation process does not generate the image file or reference it via a tag in the XML.

Related discussion: https://github.com/orgs/executablebooks/discussions/1096


How about embedding an interactive?



```{code-cell} python

import py3Dmol
view = py3Dmol.view(query='pdb:1ubq')
view.setStyle({'sphere':{'radius':'0.5'}})
view.setBackgroundColor('0x0eeeee')
#view.write_html("py3dmoldemo.html")
```


<div id="3dmolviewer_16990349875242932"  style="position: relative; width: 640px; height: 480px;">
        <p id="3dmolwarning_16990349875242932" style="background-color:#ffcccc;color:black">You appear to be running in JupyterLab (or JavaScript failed to load for some other reason).  You need to install the 3dmol extension: <br>
        <tt>jupyter labextension install jupyterlab_3dmol</tt></p>
        </div>
<script>

var loadScriptAsync = function(uri){
  return new Promise((resolve, reject) => {
    //this is to ignore the existence of requirejs amd
    var savedexports, savedmodule;
    if (typeof exports !== 'undefined') savedexports = exports;
    else exports = {}
    if (typeof module !== 'undefined') savedmodule = module;
    else module = {}

    var tag = document.createElement('script');
    tag.src = uri;
    tag.async = true;
    tag.onload = () => {
        exports = savedexports;
        module = savedmodule;
        resolve();
    };
  var firstScriptTag = document.getElementsByTagName('script')[0];
  firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
});
};

if(typeof $3Dmolpromise === 'undefined') {
$3Dmolpromise = null;
  $3Dmolpromise = loadScriptAsync('https://cdnjs.cloudflare.com/ajax/libs/3Dmol/2.0.4/3Dmol-min.js');
}

var viewer_16990349875242932 = null;
var warn = document.getElementById("3dmolwarning_16990349875242932");
if(warn) {
    warn.parentNode.removeChild(warn);
}
$3Dmolpromise.then(function() {
viewer_16990349875242932 = $3Dmol.createViewer(document.getElementById("3dmolviewer_16990349875242932"),{backgroundColor:"white"});
$3Dmol.download("pdb:1ubq", viewer_16990349875242932, {}, function() {
viewer_16990349875242932.zoomTo();
	viewer_16990349875242932.setStyle({"sphere": {"radius": "0.5"}});
	viewer_16990349875242932.setBackgroundColor("0x0eeeee");
viewer_16990349875242932.render();
})
});
</script>





+++ {"tags": ["code-cell-output"]}

<py3Dmol.view at 0x105926310>

+++




```{code-cell} python


```
