# Trying out the environment

You can try out the workflow in pre-configured environment using a `.devcontainer` in a VS Code environment running on your own computer, or in GitHub Codespaces.

## Build process

The build process for generating OU-XML from markdown is a two step process.

The first step is to generate a Sphinx XML version of the Jupyter Book, as defined by the `_toc.yml` and `_config.yml` file:

`jb build . --builder custom --custom-builder xml`

The second step is to use the [`ou-book-theme`](https://pypi.org/project/ou-book-theme/) Python package to convert the Sphinx XML to OU-XML:

`obt convert-to-ouxml .`

*NB I think release version of `ou-book-theme` is laggiong the modified version I have been working on...*

Generated OU-XML content could then be validated against an OU-XML schema by running the command:

`ou_xml_validator validate  path/to/testme.xml`

## TO DO

`````text

```{exercise}
:label: my-exercise

Recall that $n!$ is read as "$n$ factorial" and defined as
$n! = n \times (n - 1) \times \cdots \times 2 \times 1$.

There are functions to compute this in various modules, but let's
write our own version as an exercise.

In particular, write a function `factorial` such that `factorial(n)` returns $n!$
for any positive integer $n$.
```

````{solution} my-exercise
:label: my-solution

Here's one solution.

```{code-block} python
def factorial(n):
    k = 1
    for i in range(n):
        k = k * (i + 1)
    return k

factorial(4)
```
````

`````

More