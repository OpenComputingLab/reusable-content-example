# Introduction

Writing software guides to support educational modules adds authoring, editing and testing overheads to module production. If multiple modules use similar environments or software applications, reusing generic or customisable materials provides a way or reducing those overheads.

This informal report describes the production route for a customisable software guide to support the use of virtual computing environments (VCEs) across several modules. The VCEs are accessed as a remotely hosted environment provided by the Open University *Compute Home* service, or as a locally run Docker container. The method for getting started using the enviromment is likely to be the same across many modules, which suggests an opportunity for reusing generic *getting started* material. However, different modules may also vary in the sfotware provided by the VCE, which means that some degree of bespoke software guide style support material may also be required.

A common production route for the software guides required for three separate modules was explored:

- [*M348 Applied statistical modelling*](https://www.open.ac.uk/courses/modules/m348), which provides a classic Jupyter notebook environment running an R kernel;
- [*TM129 Technologies in practice (Robotics block)*](https://www.open.ac.uk/courses/modules/tm129), which provides a classic Jupyter notebook environment running an Python kernel and a simple notebook based robot simulation environment;
- [*TM351 Data management and analysis*](https://www.open.ac.uk/courses/modules/tm351), which provides a JupyterLab environment running a Python kernel, PostgreSQL and MongoDB database services, and the OpenRefine data-cleaning application.

At a technical level main aims were to explore:

- a markdown authoring route;
- a viable markdown to OU-XML conversion route;
- examples of direct publication from markdown to various output formats (HTML, PDF).

At a content production level, the main aims were to:

- maximise the amount of directly reusable content;
- explore the use of reusable customisable content;
- explore ways of integrating module specific content.

The use of several tools to support quality processes (markdown linting, spellchecking, OU-XML validation) was also explored.

The source repository for the source content can be found here: [innovationOUtside/vce-generic-guide](https://github.com/innovationOUtside/vce-generic-guide).

Example OU-XML automatically generated from the same source markdown can be viewed here: [https://opencomputinglab.github.io/reusable-content-example//ouxmlxxx_b0_p1_zzz.xml](https://opencomputinglab.github.io/reusable-content-example//ouxmlxxx_b0_p1_zzz.xml)

An HTML version rendered from the same source markdown by a Jupyter Book publication process is available here: [https://opencomputinglab.github.io/reusable-content-example/](https://opencomputinglab.github.io/reusable-content-example/)

*__Acknowledgements__: thanks to Karen Vines for helping iterate the text, Edith Francis for helping iterate the OU-XML, and Mark Hall for the original markdown2ou-xml converter.*