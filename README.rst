Contrail Documentation
======================

This repository stores documentation for OpenContrail in reStructuredText (RST) format. Each deliverable ("book") is in one subdirectory of the docs folder. 

Prerequisites
-------------

* Python: https://www.python.org/downloads/ (tested with v3.6.5, 32 bit Windows)

* Sphinx: http://www.sphinx-doc.org/en/stable/install.html (tested with v1.7.4)

Generating the documentation
----------------------------

In order to generate the documentation, after installing Python and Sphinx, execute the following commands:

1. ``cd *doc-dir*``

   where *doc-dir* is the directory containing the documentation deliverable. For example: cd contrail-docs/doc/getting-started-guide

2. ``sphinx-build . output``

   This command uses the default ``-b html`` option to build HTML. The output HTML will be placed in the subdirectory ``output``, which is ignored by Git due to an entry in the .gitignore file.
