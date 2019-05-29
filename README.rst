Contrail Documentation
======================

This repository stores documentation for OpenContrail in reStructuredText (RST) format. Each deliverable ("book") is in one subdirectory of the docs folder.

!!CAVEATS!!
-----------

Currently the documentation is either completely or partially about Contrail rather than Tungsten Fabric. We are transitioning this documentation to Tungsten Fabric and updating references and links accordingly.

This is a work in progress. 

Feel free to use the documentation in this repository but do not link to it, as it will not always be available in this location. The documents will move when the transition to Tungsten Fabric is complete.

When the work is complete, the content will be moved to the `docs` repo on `gerrit.tungsten.io`.

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
