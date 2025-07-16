# Shiny-Lite demo

The Shiny framework, originally developed for R, provides tooling for publishing interactive apps powered by backend Python or R code. The [*Shinylive*](https://shiny.posit.co/py/docs/shinylive.html) provide allows the code to be executed via a WASM backend (Python or R).
 
This suggests a workflow for creating simple apps from Python (or R) code using the *Shinylive* framework. For example, we can imagine using an `{ou-codestyle}` admonition with a `:type: shinylite-py` setting that allows code included in markdown source documents to be used as the application code in a *ShinyLive* application (misnamed as *ShinyLite* below).

For example, we could define a Shiny app as straightforwardly as including something like the following admonition in our markdown source document:

```{ou-codestyle} python
:type: shinylite-py
from shiny import App, render, ui

app_ui = ui.page_fluid(
    ui.panel_title("Hello Demo Shiny!"),
    ui.input_slider("n", "N", 0, 100, 20),
    ui.output_text_verbatim("txt"),
)

def server(input, output, session):
    @render.text
    def txt():
        return f"n*2 is {input.n() * 2}"

app = App(app_ui, server)

```

```{ou-codestyle} python
:type: shinylite-py
from shiny import App, render, ui

app_ui = ui.page_fluid(
    ui.panel_title("Hello Demo Shiny!"),
    ui.input_slider("n", "N", 0, 100, 20),
    ui.output_text_verbatim("txt"),
)

def server(input, output, session):
    @render.text
    def txt():
        return f"n*2 is {input.n() * 2}"

app = App(app_ui, server)

```

The application should then be rendered directly into the page.

__DEMO STATUS: BROKEN__

*In the set up I am using, everything is vendored. At least one of the current issues is the value to download the .wasm file due to an incorrect MIME-type (`.wasm` should be served as `application/wasm`). I also recall having MIME-type issues with `.mjs`, which should be served as `text/javascript`.*
