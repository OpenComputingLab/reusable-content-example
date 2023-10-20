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

# Authoring reusable content

To start the authoring process, a legacy software guide available as an OU-XML structured content document was rendered to simple markdown.

Sphinx style configuration and table of contents scripts were created to so that the content could be previewed in an HTML book style format, or rendered back to OU-XML.

Several features of Sphinx style publishing that support extensibility and reuse were adopted that allowed us to trade-off purely generic content, customisable content, and bespoke content for each module.

## Table of Contents Configuration Files

From a set of content files, one of the easiest ways of defining which content files are to be used to generate a particular output document is to specify the files that are to be included via a table of contents file.

In current production workflows, it would not be unusual for each module team author to their own software guide. In a markdown workflow, this might include each module team authoring several separate markdown documents, many of which may  duplicate similar instructional intent, and then create their own table of contents files to use their authored documents.

One obvious way of reusing content across several modules would be for each module to use exactly the same guide, where the same table of contents file pulls from the same source documents.

Partial customisation might be supported by each module team writing their own introduction, for example, but reusing all the other sections of the guide.  The output document is then defined using a module specific table of contents file that pulls in the module specific content (for example, from the file `introduction-XY123.md`) as well as a the generic reusable content files.

When writing this sort of content, we must try to avoid making any references to a particular module. Where references to a module code are required, one possible approach is to use a generic code (for example `XY123`, or `XXNNN`) and then tell a student to use apply their particular module code in place of the generic code.

For example, two modules might reuse content from a set of common files, as well as featuring module specific content, using the following table of contents files:

```yaml
format: jb-book
root: g-vce_cribsheet
chapters:
  - file: g-introduction-m348
  - file: g-compute_home
  - file: g-local_vce_quickstart
```

```yaml
format: jb-book
root: g-vce_cribsheet
chapters:
  - file: g-introduction-tm351
  - file: g-compute_home
  - file: g-local_vce_quickstart
```

## Transcluding / Embedding content

One of the nice features of the Sphinx publishing workflow is that content files can import content from other content files. This allows us to define "partial" files that might include the content of just a single paragraph, for example.

A module specific file can then be defined that includes module specific text (either imported from a partial content file or explicitly provided inline within the file) as well as generic text imported from a reusable partial content file.

For example, the following markdown fragment shows how we might customise a module specific introduction file by first loading in generic content from a reusable file, and then appending some module specific content.

````text
```{include} ./g-introduction-core.md

Finally, we have a conclusion paragraph that speaks to a particular module.
```
````

## Parameterised Customisable Content

In many cases, whilst the content is predominantly reusable, there may be a requirement to customise it for use in particular module by referring to the module code or module name.

In this case, rather than generate a custom file for each module, we can simply parameterise the module code, module name, etc., and then define a module configuration file that sets a generic module name placeholder label, for example, to a required module name.

For example, the following raw markdown fragment shows how we can use parameterised values at the start of a generic, customisable "cribsheet" document.

```text
# Virtual Computing Environment Cribsheet ({{module_code}}, {{presentation_code}} Presentation)

## VCE Cribsheet

- Module code: {{module_code}}
- Presentation code: {{presentation_code}}
```

The configuration file allows the definition of variables as well as some limited processing of those variables (for example, casting to upper or lower case) as part of further configuration elements.

```text
myst_substitutions:
    MCODE: M348
    NCODE: "348"
    MNAME: "Applied Statistical Modelling"
    PCODE: 23J
    YEAR: "2023"
    jupyter_help_forum: "'Jupyter notebooks' forum"

    # DEFAULT VALUES / RULES
    module_code: "{{'`' + MCODE|upper + '`'}}"
    presentation_code: "{{'`' + PCODE|upper + '`'}}"
```
