# Truphone Connect usage documentation

This documentation is written in standard markdown and built using the [Read The Docs format](https://readthedocs.org/) for the [Sphinx](http://www.sphinx-doc.org/en/master/) python documentation generator.

## How to setup local development
Assuming you already have python installed:

```bash
pip install sphinx
pip install sphinx_rtd_theme
pip install recommonmark
pip install sphinx-markdown-tables
```

Sphinx is now ready to build the documentation

## Writing documentation
Documentation is written using the standard markdown format. Markdown files are stored under the source/** directories. VSCode and IntelliJ have good support for editing markdown files

## Generating the docs
```bash
make html
```
Generated documentation will be stored under build/docs/html/index.html
