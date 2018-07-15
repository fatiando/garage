.. raw:: html

    <h1 align="center">
        <strong>Garage</strong>
    </h1>

    <h3 align="center">
        <strong>A place to park your sample data files.</strong>
    </h3>

    <p align="center">
    <a href="https://pypi.python.org/pypi/garage"><img alt="Latest version on PyPI" src="http://img.shields.io/pypi/v/garage.svg?style=flat-square"></a>
    <a href="https://travis-ci.org/fatiando/garage"><img alt="TravisCI build status" src="http://img.shields.io/travis/fatiando/garage/master.svg?style=flat-square&label=Linux|Mac"></a>
    <a href="https://ci.appveyor.com/project/fatiando/garage"><img alt="AppVeyor build status" src="http://img.shields.io/appveyor/ci/fatiando/garage/master.svg?style=flat-square&label=Windows"></a>
    <a href="https://codecov.io/gh/fatiando/garage"><img alt="Test coverage status" src="https://img.shields.io/codecov/c/github/fatiando/garage/master.svg?style=flat-square"></a>
    <a href="https://pypi.python.org/pypi/garage"><img alt="Compatible Python versions." src="https://img.shields.io/pypi/pyversions/garage.svg?style=flat-square"></a>
    <a href="https://gitter.im/fatiando/fatiando"><img alt="Chat room on Gitter" src="https://img.shields.io/gitter/room/fatiando/fatiando.svg?style=flat-square"></a>
    </p>

    <p align="center">
    <a href="http://www.fatiando.org/garage">Documentation</a> |
    <a href="https://gitter.im/fatiando/fatiando">Contact</a> |
    Part of the <a href="https://www.fatiando.org">Fatiando a Terra</a> project
    </p>


TL;DR
-----

.. code:: python

    """
    Module mypackage/datasets.py
    """
    import garage

    # Get the version string from your project. You have one of these, right?
    from . import __version__

    # Check if this is a valid version number (PEP 440). If not, then return the fallback.
    # Needed to have versioned data and not mess things up when updating data on master.
    version = garage.check_version(__version__, fallback="master")

    # Create a new garage to manage your sample data storage
    STORAGE = garage.create(
        # Folder where the data will be stored. We'll join lists using os.path for you.
        folder=[".myproject", "data", version],
        # Base directory for the data folder. If None, will use the $HOME env variable.
        base_dir=None,
        # Name of an environment variable that overwrites the location of the data folder.
        env_variable="MYPROJECT_DATA_DIR",
        # Base URL of the remote data store. Only supports HTTP for now.
        base_url="https://github.com/me/myproject/raw/{}/data/".format(version)
    )


    def fetch_some_data():
        """
        Load some sample data to use in your docs.
        """
        # Get the path to a file in the garage. If it's not there, we'll download it.
        fname = STORAGE.fetch("some-data.csv", sha256="0981jdkjo2h0d2hdljh982wd2dpoj0")
        # Load it with numpy/pandas/etc
        data = ...
        return data



About
-----

*Does your Python package include sample datasets? Are you shipping them with the code?
Are they getting too big?*

Garage will manage downloading your sample data files over HTTP from a server and
storing them in a local directory:

* Download a file only if it's not in the local garage.
* Check the SHA256 hash to make sure the file is not corrupted or needs updating.
* If the hash is different Garage will download a new version of the file.
* If the hash still doesn't match, Garage will warn of possible data corruption.
* If no hash is given, Garage won't perform any checks.


Contacting Us
-------------

* Most discussion happens `on Github <https://github.com/fatiando/garage>`__.
  Feel free to `open an issue
  <https://github.com/fatiando/garage/issues/new>`__ or comment
  on any open issue or pull request.
* We have `chat room on Gitter <https://gitter.im/fatiando/fatiando>`__ where you can
  ask questions and leave comments.


Contributing
------------

Code of conduct
+++++++++++++++

Please note that this project is released with a
`Contributor Code of Conduct <https://github.com/fatiando/garage/blob/master/CODE_OF_CONDUCT.md>`__.
By participating in this project you agree to abide by its terms.

Contributing Guidelines
+++++++++++++++++++++++

Please read our
`Contributing Guide <https://github.com/fatiando/garage/blob/master/CONTRIBUTING.md>`__
to see how you can help and give feedback.

Imposter syndrome disclaimer
++++++++++++++++++++++++++++

**We want your help.** No, really.

There may be a little voice inside your head that is telling you that you're
not ready to be an open source contributor; that your skills aren't nearly good
enough to contribute.
What could you possibly offer?

We assure you that the little voice in your head is wrong.

**Being a contributor doesn't just mean writing code**.
Equality important contributions include:
writing or proof-reading documentation, suggesting or implementing tests, or
even giving feedback about the project (including giving feedback about the
contribution process).
If you're coming to the project with fresh eyes, you might see the errors and
assumptions that seasoned contributors have glossed over.
If you can write any code at all, you can contribute code to open source.
We are constantly trying out new skills, making mistakes, and learning from
those mistakes.
That's how we all improve and we are happy to help others learn.

*This disclaimer was adapted from the*
`MetPy project <https://github.com/Unidata/MetPy>`__.


License
-------

This is free software: you can redistribute it and/or modify it under the terms
of the **BSD 3-clause License**. A copy of this license is provided in
``LICENSE.txt``.

