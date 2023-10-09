# reusable-content-example

Informal report on creating reusable / generic content as Markdown text with conversion to OU-XML


## Build process

Generate the Sphinx XML version of the Jupyter Book, as defined by the `_toc.yml` and `_config.yml` file:

`jb build . --builder custom --custom-builder xml`

Convert to OU-XML:

`obt convert-to-ouxml .`

## `.devcontainer` Set-up

The `.devcontainer` set up allows you to run the build tools ... TO DO