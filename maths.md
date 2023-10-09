# Maths

Mathematical equations written using LaTeX syntac can be specified inline or as a block level equation.

For example, the inline equation {math}`e=mc^2` is specified in mardown using the `{math}` role: `` {math}`e=mc^2` ``

We can also use a `{math}` directive to define an equation block:

````text
```{math}
:label: my-equation-identifier
w_{t+1} = (1 + r_{t+1})
s(w_t) + y_{t+1}
```
````

```{math}
:label: my-equation
w_{t+1} = (1 + r_{t+1})
s(w_t) + y_{t+1}
```

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

The `$$` syntax also works as a one-liner. For example, the single line:

`$$ \label{one-liner} Ax=b $$`

will ultimately render as the formatted equation:

$$ \label{one-liner} Ax=b $$
