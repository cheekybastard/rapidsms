Running the RapidSMS core test suite
====================================

RapidSMS uses `nose <http://pypi.python.org/pypi/nose/>`_ to run its test suite
and provides several configuration options and entry points for continuous
integration. The unit tests can be run in the current python environment or
automated to run in several environments and can include coverage reports.

Quickstart
----------

The easiest way to run the unit tests in a new install is to run the following
from the project root::

    pip install ./
    pip install -r tests/requirements/base.txt
    python run_tests.py --settings=tests.default

The settings found in the /tests/default.py module are intended as the default
settings file for running tests. You can tell the test runner what settings
file to use with the --settings flag or by setting your
``DJANGO_SETTINGS_MODULE`` environment variable.

Testing multiple environments
-----------------------------

RapidSMS uses `Tox <http://tox.readthedocs.org/en/latest/index.html>`_ to run
the test suite in a variety of environments. The environments included in the
tox.ini file are:

 * ``py26-1.3.X`` - Test using Python 2.6 and Django 1.3.X
 * ``py26-1.4.X`` - Test using Python 2.6 and Django 1.4.X
 * ``py26-trunk`` - Test using Python 2.6 and Django master
 * ``py27-1.3.X`` - Test using Python 2.7 and Django 1.3.x
 * ``py27-1.4.X`` - Test using Python 2.7 and Django 1.4.x
 * ``py27-trunk`` - Test using Python 2.7 and Django master

You can run any of the environments listed above using: ``tox -e <name>``.
Using ``tox`` on its own runs the test suite against all environments.

You can also add additional environments or change other parts of the
configuration in your local copy of the tox.ini by following the `tox
configuration specification
<http://tox.readthedocs.org/en/latest/config.html>`_ docs.

Continuous integration and coverage reports
-------------------------------------------

If desired, the test suite can produce a Cobertura coverage report for use with
continuous integration software. Setting the environment variable CI to 1
before running the test suite will produce a coverage report in the
coverage.xml file. For example, the following produces a coverage.xml file and
prints a coverage report for the test suite in the current environment::

	CI=1; ./run_tests.py

If you are using tox, this environment variable is set to 1 automatically.

Using setup.py
--------------

Your ``DJANGO_SETTINGS_MODULE`` must be set in order for the test suite using
setup.py. Running the following will install test dependencies and run the unit
tests in one step, but without the option of a coverage report::

    export DJANGO_SETTINGS_MODULE=tests.default
    ./setup.py test
