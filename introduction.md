# Introduction

Writing software guides to support educational modules adds authoring, editing and testing overheads to module production. If multiple modules use similar environments or software applications, reusing generic or customisable materials provides a way or reducing those overheads.

This informal report describes the production route for a customisable software guide to support the use of virtual computing environments (VCEs) across several modules.

The VCEs are accessed as a remotely hosted environment provided by the Open University *Compute Home* service, or as a locally run Docker container. *The same Docker image should ideally be used to support both the hosted and locally run environment.*

A common production route for the software guides required for three separate modules was explored:

- [*M348 Applied statistical modelling*](https://www.open.ac.uk/courses/modules/m348), which provides a classic Jupyter notebook environment running an R kernel;
- [*TM129 Technologies in practice (Robotics block)*](https://www.open.ac.uk/courses/modules/tm129), which provides a classic Jupyter notebook environment running an Python kernel and a simple notebook based robot simulation environment;
- [*TM351 Data management and analysis*](https://www.open.ac.uk/courses/modules/tm351), which provides a JupyterLab environment running a Python kernel, PostgreSQL and MongoDB database services, and the OpenRefine data-cleaning application.

The main aims were:

- to maximise the amount of directly reusable content;
- to explore the use of reusable customisable content;
- to explore ways of integrating module specific content.

In addition, the work demonstrated a markdown-based authoring route with an automated conversion process capable of producing output assets in various formats (OU-XML (for use in OU production workflows: VLE rendering, PDF creation); HTML book format; simple PDF preview). The use of several tools to support quality processes (markdown linting, spellchecking, OU-XML validation) were also explored.

The source repository for the source content can be found here: [innovationOUtside/vce-generic-guide](https://github.com/innovationOUtside/vce-generic-guide).

*__Acknowledgements__: thanks to Karen Vines for helping iterate the text, Edith Francis for helping iterate the OU-XML, and Mark Hall for the original markdown2ou-xml converter.*