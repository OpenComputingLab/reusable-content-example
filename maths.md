# Maths

Mathematical equations written using LaTeX syntax can be specified inline or as a block level equation.

For example, the inline equation {math}`e=mc^2` is specified in markdown using the `{math}` role: `` {math}`e=mc^2` ``

We can also use a `{math}` directive to define an equation block:

````text
```{math}
:label: my-equation
w_{t+1} = (1 + r_{t+1})
s(w_t) + y_{t+1}
```
````

```{math}
---
label: my-equation
---
w_{t+1} = (1 + r_{t+1})
s(w_t) + y_{t+1}
```

These corresponding OU-XML is then a `<ProgramListing>` to show the script that is used to defined the equation, and an `Equation` block from which the rendered equation can be generated:

````xml
<ProgramListing>
    <Paragraph>```{math}</Paragraph>
    <Paragraph>:label: my-equation</Paragraph>
    <Paragraph>w_{t+1} = (1 + r_{t+1})</Paragraph>
    <Paragraph>s(w_t) + y_{t+1}</Paragraph>
    <Paragraph>```</Paragraph>
</ProgramListing>
        
<Equation id="my-equation">
    <TeX>w_{t+1} = (1 + r_{t+1})
s(w_t) + y_{t+1}</TeX>
</Equation>
````

Dollar math syntax may also be used to define block equations:

```text
$$
\label{maxwell}
\begin{aligned}
\nabla \times \vec{e}+\frac{\partial \vec{b}}{\partial t}&=0 \\
\nabla \times \vec{h}-\vec{j}&=\vec{s}\_{e}
\end{aligned}
$$
```

$$
\label{maxwell}
\begin{aligned}
\nabla \times \vec{e}+\frac{\partial \vec{b}}{\partial t}&=0 \\
\nabla \times \vec{h}-\vec{j}&=\vec{s}\_{e}
\end{aligned}
$$

In OU-XML, we again render the two elements above as a listing and an equation type:

```xml
<ProgramListing>
    <Paragraph>$$</Paragraph>
    <Paragraph>\label{maxwell}</Paragraph>
    <Paragraph>\begin{aligned}</Paragraph>
    <Paragraph>\nabla \times \vec{e}+\frac{\partial \vec{b}}{\partial t}&amp;amp;=0 \\</Paragraph>
    <Paragraph>\nabla \times \vec{h}-\vec{j}&amp;amp;=\vec{s}\_{e}</Paragraph><Paragraph>\end{aligned}</Paragraph
    ><Paragraph>$$</Paragraph>
</ProgramListing>

<Equation>
    <TeX>
        \label{maxwell}
        \begin{aligned}
        \nabla \times \vec{e}+\frac{\partial \vec{b}}{\partial t}&amp;=0 \
        \nabla \times \vec{h}-\vec{j}&amp;=\vec{s}_{e}
        \end{aligned}
    </TeX>
</Equation>
```

The `$$` syntax also works as a one-liner. For example, the single line:

`$$ \label{one-liner} Ax=b $$`

will ultimately render as the formatted equation:

$$ \label{one-liner} Ax=b $$
