How to contribute to the documentation
======================================

This guide will explain how you can update and expand the documentation.

Prerequisites
-------------

We use `Sphinx <https://www.sphinx-doc.org/en/master/>`_ to generate this documentation,
so while it is not strictly necessary to be able to contribute it is a good idea to
first learn the basics of `how Sphinx works
<https://www.sphinx-doc.org/en/master/tutorial/getting-started.html>`_ in case you are
not familiar with it.

Sphinx uses `reStructuredText (reST)
<https://www.writethedocs.org/guide/writing/reStructuredText/>`_ as its default markup
language and our documentation is largely written in reST. You can the `reST
reference <https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_ to
look up syntax and directives as needed when editing the documentation.

Updating the API reference
--------------------------

The :doc:`API reference <../api>` is generated automatically from python docstrings
using the `autosummary
<https://www.sphinx-doc.org/en/master/usage/extensions/autosummary.html>`_ Sphinx
extension. Therefore, to update this part of the documentation it is enough to update
the respective docstrings. See :ref:`updating-docstrings` for the docstring conventions
we use.

.. _updating-docstrings:

Updating docstrings
^^^^^^^^^^^^^^^^^^^

Every function or class should have a docstring explaning its use. We use the `numpy
documentation style <https://numpydoc.readthedocs.io/en/latest/format.html>`_ to write
the docstrings. Since the API refenrence is then generated with Sphinx, you can add
additional reST directives (such as todos, warnings, maths, ...) which will then be
rendered on the documentation website.


Updating the rest of the documentation
--------------------------------------

The :doc:`Overview <../overview/index>`, :doc:`Getting Started <../tutorial/index>` and
:doc:`How-to guides <../howto/index>` parts of the documentation have to be written
manually.

The source code of the documentation is versioned in git with the rest of the code of
the repository in the `docs/source
<https://github.com/tibor-mach/semal/tree/main/docs>`_ directory, so just edit the
relevant ``.rst`` files there.

.. seealso::
    For the list of things that definitely need some work in the documentation
    check out the :doc:`To do list <../todos>`.

Viewing changes to the documentation
------------------------------------

For its autodoc function which parses docstrings from Python code, Sphinx actually needs
to run the code. This means that you need to install all dependencies used in the
documented code before building documentation. All such dependencies are already listed
in ``pyproject.toml`` in the root of the repository. They can be easily installed into
a virtual environment by using the ``make venv`` command from the Makefile in the root
of the repository.

.. warning::
    Because sphinx executes code whe building documentation, make sure that all scripts
    you want to include in the API reference have the executed part of the code wrapped
    within the following code

    .. code:: python

        if __name__ == "__main__:"


Once you've made some edits, the simplest way to build the documentation webpages is to
use the existing ``Makefile`` in the ``docs`` directory of the repository.

To view the changes you made you can either open the local
``docs/build/html/index.html`` file in your web browser (and refresh it as you make
changes to the source code and ``make html`` new files) or if you're feeling fancy you
can set up a local development server. In the latter case you can follow `this guide
<https://pradyunsg.me/furo/contributing/workflow/#local-development-server>`_.

Once you are happy with the changes, create a pull request as you would with any other
change to the repository. Once your changes are merged to the main branch the website
will be deployed online using a GitHub Actions workflow.
