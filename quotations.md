# Quotations

We can define quotations in markdown by prefix the quoted line or lines with a `>` symbol at the start of the line:

This works for single line quotes:

`> Here is a single line quote.`

> Here is a single line quote.

which are rendered in OU-XML as:

```xml
<Quote><Paragraph>Here is a single line quote.</Paragraph></Quote>
```

and multi-line quotes:

```text
> Here is the first line of the quote...
> ...and here is the second.
>
> And a final line.
```

which are rendered in OU-XML as:

```xml
<Quote>
    <Paragraph>Here is the first line of the quote…
    …and here is the second.</Paragraph>
<Paragraph>And a final line.</Paragraph>
</Quote>

```

The following is a quote and should be marked up as such:

> Here is the first line of the quote...
> ...and here is the second.
>
> And a final line.

The following is a quote that should be marked up as such, along with a typographically distinguished source reference component:

> Here is the first line of the quote...
> ...and here is the second.
>
> Source: And a final line source...

The source markdown is:

```text
> Here is the first line of the quote...
> ...and here is the second.
>
> Source: And a final line source...
```

In OU-XML, we get:

```xml
<Quote><Paragraph>Here is the first line of the quote…
                …and here is the second.</Paragraph><SourceReference>And a final line source…</SourceReference></Quote>
```
