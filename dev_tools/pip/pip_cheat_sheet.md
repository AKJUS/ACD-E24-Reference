# pip cheat sheet

pip installs Python packages, usually from the Python Package Index (PyPI).
Activate the intended environment before using these commands. Use `python -m pip`
so pip runs through that environment's Python interpreter; a bare `pip` command
or the Windows `py` launcher may resolve to a different installation.

**Contents:** [Interpreter](#check-the-target-interpreter) · [Installation](#install-packages)
· [Versions](#specify-versions) · [Inspection](#inspect-and-verify) · [Maintenance](#update-or-remove-packages)
· [Dependency files](#use-requirements-files) · [Conda and pip](#combine-conda-and-pip)
· [Troubleshooting](#quick-diagnosis)

## Check the target interpreter

For the course environment:

```sh
conda activate acd
python -c "import sys; print(sys.executable)"
python -m pip --version
```

The Python executable and pip location should belong to the same environment.
Use another environment name for a separate project or experiment, and select
that interpreter in VS Code as well. If pip is absent from a Conda environment,
install it there with `conda install -n ENVIRONMENT_NAME pip`, replacing the name.

## Install packages

The commands below are alternatives for different situations. NetworkX is an
example additional library; use the installation name given in your library's
documentation.

| Task | Command |
| --- | --- |
| Install a compatible release | `python -m pip install networkx` |
| Install several packages together | `python -m pip install networkx sympy` |
| Preview dependency resolution without installing | `python -m pip install --dry-run networkx` |
| Read installation options | `python -m pip install --help` |

pip manages Python distributions; it does not create environments or install a
different Python interpreter. For a Conda environment, follow the
[combined package-manager workflow](#combine-conda-and-pip).

## Specify versions

| Requirement | Command |
| --- | --- |
| Exact release | `python -m pip install "numpy==1.26.4"` |
| Minimum version | `python -m pip install "numpy>=1.26"` |
| Bounded range | `python -m pip install "numpy>=1.26,<2"` |
| Patch releases within a series | `python -m pip install "numpy==1.26.*"` |

These versions illustrate the syntax; preserve an existing project's requirements.
Use `==` for an exact pip version. A single `=` is not valid pip version syntax.
Quote constraints in terminal commands, particularly those containing `<` or `>`.
A requested release must support your Python version and operating system.

## Inspect and verify

| Task | Command |
| --- | --- |
| List installed Python distributions | `python -m pip list` |
| Show a package's version, location, and dependencies | `python -m pip show networkx` |
| List packages with newer available releases | `python -m pip list --outdated` |
| Check installed dependency requirements | `python -m pip check` |
| Read pip's general help | `python -m pip --help` |

Verify that the package can be imported with the intended interpreter:

```sh
python -c "import networkx; print(networkx.__version__)"
```

Installation names and import names can differ: install `scikit-image`, for
example, but import `skimage`. A successful `pip check` confirms declared
dependency compatibility; also run the code that uses the package.

## Update or remove packages

| Task | Command |
| --- | --- |
| Upgrade a pip-installed package | `python -m pip install --upgrade networkx` |
| Upgrade while retaining a version range | `python -m pip install --upgrade "networkx>=3,<4"` |
| Select a specific compatible version | `python -m pip install "networkx==3.2.1"` |
| Remove a pip-installed package | `python -m pip uninstall networkx` |

Without `--upgrade`, pip may keep an installed release that already satisfies
the requirement. An upgrade can change dependencies; verify the affected code
afterward. Uninstalling a package does not automatically remove all of its
dependencies. Use Conda to remove packages originally installed with Conda.

## Use requirements files

A requirements file contains one requirement per line. For example:

```text
numpy>=1.26,<2
networkx>=3,<4
```

Save the text as `requirements.txt`. Entries in the file do not use shell quotation
marks. Run the following from its directory, or supply the file's path:

```sh
python -m pip install -r requirements.txt
```

For a project managed primarily with pip, record the currently installed versions:

```sh
python -m pip freeze > requirements-snapshot.txt
```

Reinstall those versions in another compatible environment:

```sh
python -m pip install -r requirements-snapshot.txt
```

`freeze` records installed Python distributions, including indirect dependencies.
It does not record the Python interpreter or all non-Python libraries and is not
a complete Conda environment specification. The `>` operator overwrites an
existing file of the same name.

## Combine Conda and pip

Install the Conda dependencies first, then use pip for packages required from PyPI
or another supported Python package source. Avoid repeatedly replacing the same
package with both managers: Conda may not account for every change made by pip.
Record the combined specification; if further Conda changes are needed, recreate
the environment from that specification. Use the package manager that installed
a package when removing it.


A Conda environment file can include a pip section. This example installs the
interpreter and NumPy with Conda, then NetworkX with pip:

```yaml
name: library-test
channels:
  - conda-forge
  - nodefaults
dependencies:
  - python=3.11
  - numpy=1.26
  - pip
  - pip:
      - networkx>=3,<4
```

Save it as `library-test.yml` and create a new environment from it with
`conda env create -f library-test.yml`. Choose a new name or remove the previous
test environment first if `library-test` already exists. Keep the dependencies
you intentionally add recorded alongside the project that needs them.

## Quick diagnosis

| Symptom | First check |
| --- | --- |
| Installation succeeds but the import fails | Compare `sys.executable`, pip's location, the editor interpreter, and the import name. |
| `No module named pip` | Install pip into the selected Conda environment. |
| `No matching distribution found` | Check the installation name, version constraint, Python version, and operating system. |
| Dependencies conflict | Read the conflicting requirements and test a compatible set in a separate environment. |
| Permission or externally managed environment error | Verify that Python belongs to your own environment rather than the system installation. |
| Source build fails | Check the library's installation instructions for compatible prebuilt packages or required build tools. |
