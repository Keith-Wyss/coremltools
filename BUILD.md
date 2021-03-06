### Building from Source

To build the project, you need [CMake](https://cmake.org) to configure the project.

```shell
./configure
```

When several python virtual environments are installed, it may be useful to
point to the correct intended version of python (see `./configure --help` for
options)

The configure script creates a virtual environment. You can source the right
environment variables using

```
source ./scripts/python_env.sh
```

Now you can build the package as follows:

```shell
cmake -H. -Bbuild
make -C build -j3
```

Then you can install it into your virtualenv:

```shell
pip install -e .
```
### Running Unit Tests

You can run all the unite tests using the following command.

```shell
pytest -rfs -m "not slow" coremltools/test
```
See [pytest documentation](https://docs.pytest.org/en/latest/) to learn more
about how to run a single unit test.

If you would like a wheel to install outside of the virtualenv, 
use `make -C build dist` and find the resulting wheels in `build/dist/*.whl`.

If you want to build a wheel for distribution or testing, there is a script
that automates all of the steps necessary for building a wheel,
`scripts/make_wheel.sh`, that can be used instead (but make sure to install the
wheel before running unit tests, if you plan to run the tests).

### Building Documentation

First install all external dependencies.

```shell
pip install Sphinx==1.8.5 sphinx-rtd-theme==0.4.3 numpydoc==0.9.1
pip install -e git+git://github.com/michaeljones/sphinx-to-github.git#egg=sphinx-to-github
```
You also must have the *coremltools* package install, see the *Building*
section. Then from the root of the repository:

```shell
cd docs
make html
open _build/html/index.html
```
