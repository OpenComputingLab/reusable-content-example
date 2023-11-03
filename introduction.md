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

# Introduction

OU course materials destined for publication on the Open University VLE via the "Structured Content" OU-XML publishing route ([OU internal docs](https://learn3.open.ac.uk/mod/oucontent/view.php?id=185734)) are typically authored as Microsoft Word documents.

Updating materials using this route can often be a laborious process, with authors editing the MS Word document and then handing over the document the changes to be "tagged" elsewhere.

The current workflow is also limited in the extent to which it supports the reuse of content across modules, particularly where the content requires any form of customisation. For example, writing software guides to support educational modules adds authoring, editing and testing overheads to module production. If multiple modules use similar computer environments or software applications, reusing generic or customisable materials provides a way or reducing those overheads. Where fixes are made to generic, or "core", content in one module, this fixes should also available to other modules drawing om the same core content.

In addition, module teams often require software guides that are customised at several different levels. At an "inline" level, a module team may want the guide to refer to the module by module code or module name, or refer to a particular block of study. At a "paragraph" level, where some form of "localisation" relative to the module may be appropriate, such as situating the use of a the software environment within a particular block or module with some module specific context. Or at the "section: level, where for example the software environment may have additional, module specific features that require an additional form of guidance, or a cut-down version of the environment that does not require sections that are likely to be relevant to other modules.

Although the MS Word originated workflow has remained largely unchanged for several years, other routes into the Structured Content production *are* available. One such route is a markdown based workflow which supports the creation of markdown flavoured content and its conversion to OU-XML.

This report introduces a markdown based publication route that uses a Sphinx-based publishing route to generate valid OU-XML Structured Content documents from markdown source documents.

The source markdown documents from which this VLE presented content was derived are available here: [`OpenComputingLab/reusable-content-example`](https://github.com/OpenComputingLab/reusable-content-example).

An HTML version rendered from the same source documents by a Jupyter Book publication process is available here: [https://opencomputinglab.github.io/reusable-content-example/](https://opencomputinglab.github.io/reusable-content-example/)

Example OU-XML automatically generated from the same source markdown can be viewed here: [generated OU-XML](https://opencomputinglab.github.io/reusable-content-example/ouxml/xxx_b0_p1_zzz.xml)

## A customisable, cross-module software guide with a markdown2OUXML production process

An earlier version of the production route has already been used in an initial proof of concept project to produce a customisable software guide to support the use of virtual computing environments (VCEs) across several modules:

- [*M348 Applied statistical modelling*](https://www.open.ac.uk/courses/modules/m348), which provides a classic Jupyter notebook environment running an R kernel;
- [*TM129 Technologies in practice (Robotics block)*](https://www.open.ac.uk/courses/modules/tm129), which provides a classic Jupyter notebook environment running an Python kernel and a simple notebook based robot simulation environment;
- [*TM351 Data management and analysis*](https://www.open.ac.uk/courses/modules/tm351), which provides a JupyterLab environment running a Python kernel, PostgreSQL and MongoDB database services, and the OpenRefine data-cleaning application.

At a technical level, the main aims of that initial project were to explore:

- a markdown authoring route;
- a viable markdown to OU-XML conversion route;
- examples of direct publication from markdown to various output formats (HTML, PDF).

At a content production level, the main aims were to:

- maximise the amount of directly reusable content;
- explore the use of reusable customisable content;
- explore ways of integrating module specific content.

The use of several tools to support quality processes (markdown linting, spellchecking, OU-XML validation) was also explored.

The source repository for the source content for the generic, customisable virtual computing environment (VCE) can be found here: [`innovationOUtside/vce-generic-guide`](https://github.com/innovationOUtside/vce-generic-guide).

The source repository for the source content for the generic, customisable virtual computing environment (VCE) software guide can be found here: [`innovationOUtside/vce-generic-guide`](https://github.com/innovationOUtside/vce-generic-guide).

*__Acknowledgements__: thanks to Karen Vines for helping iterate the text, Edith Francis for helping iterate the OU-XML, and Mark Hall for the original markdown2ou-xml converter and his insight into using Sphinx XML as a route to OU-XML.*
