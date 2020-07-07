# Truphone Connect API reference documentation

Source files for the Truphone Connect API reference documentation, hosted in this repository: [https://truphone.github.io/connect-api-docs](https://truphone.github.io/connect-api-docs) 

## Setup local development

Assuming you already have a functional python development environment:

```bash
pip install sphinx
pip install sphinx_rtd_theme
pip install recommonmark
pip install sphinx-markdown-tables
```

Sphinx is now ready to build the documentation

## Writing documentation

Documents are written in the standard markdown format, stored under the `source/` directories and built using the [Read The Docs](https://readthedocs.org/) template for the [Sphinx](http://www.sphinx-doc.org/en/master/) python documentation generator.

## Generating the html

```bash
make html
```

Generated documentation will be stored under build/docs/html/index.html

## Building for github pages

```bash
make github
```

Same as make html but also copies the files to the `docs/` folder for github to serve them.  

