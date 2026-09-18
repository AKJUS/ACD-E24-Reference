# Conda cheat sheet

Reference commands for an existing Conda installation. For installation and the
initial course environment, follow the [setup walkthrough](README.md). These
examples use `design-test`; replace it with the environment you intend to manage.
Choose the command for the task rather than running every example in order.

**Contents:** [Inspect](#inspect-environments) · [Environments](#create-and-select-an-environment)
· [Packages and versions](#install-packages-and-select-versions) · [Maintenance](#update-or-remove-packages)
· [Dependency files](#record-and-recreate-an-environment) · [Removal](#delete-an-environment)
· [Troubleshooting](#quick-diagnosis)

## Inspect environments

| Task | Command |
| --- | --- |
| List environments and their paths | `conda env list` |
| List packages in a named environment | `conda list -n design-test` |
| Find an installed package and its version | `conda list -n design-test numpy` |
| Read help for an operation | `conda create --help` |

## Create and select an environment

Create an environment with a Python release series and initial packages:

```sh
conda create -n design-test -c conda-forge python=3.11 numpy pip
conda activate design-test
```

`-n` names the environment; `-c` adds a package channel to the search. A channel
provides package builds. Specify the main dependencies together so Conda can
resolve a compatible set. Use a new name when an environment already exists.

| Task | Command |
| --- | --- |
| Create from a file under a different name | `conda env create -n design-copy -f environment.yml` |
| Clone an existing environment | `conda create -n design-copy --clone design-test` |
| Activate an environment in this terminal | `conda activate design-test` |
| Leave the active environment | `conda deactivate` |
| Run a script in a named environment without activating it | `conda run -n design-test python script.py` |

Use the directory containing `environment.yml`, or supply its path. In the last
example, replace `script.py` with your script's path. Activation selects an
interpreter; it does not change the working directory or the interpreter selected
in VS Code.

Repeat the [interpreter checks](README.md#4-verify-the-interpreter-and-imports)
after selecting a different environment, using that project's required versions
and imports.

## Install packages and select versions

These are alternative requirements. Example versions illustrate the syntax;
retain the versions specified by an existing project.

| Requirement | Command |
| --- | --- |
| Install compatible packages | `conda install -n design-test -c conda-forge numpy matplotlib` |
| Select a package release series | `conda install -n design-test -c conda-forge numpy=1.26` |
| Select an exact package release | `conda install -n design-test -c conda-forge "numpy==1.26.4"` |
| Allow a bounded range | `conda install -n design-test -c conda-forge "numpy>=1.26,<2"` |
| Create with an exact Python release | `conda create -n python-test -c conda-forge "python==3.11.9" pip` |
| Search a channel for available versions | `conda search -c conda-forge numpy` |
| Preview an installation without changing packages | `conda install -n design-test -c conda-forge numpy --dry-run` |

Conda uses `=` to match a release series and `==` to match an exact version.
Quote expressions containing comparison operators so the shell passes them through
unchanged. Requested versions must have compatible builds for the selected Python
version and operating system.

## Update or remove packages

| Task | Command |
| --- | --- |
| Update a package to a compatible version | `conda update -n design-test numpy` |
| Remove a Conda-installed package | `conda remove -n design-test numpy` |
| Apply changes from a project's specification | `conda env update -n design-test -f environment.yml` |

Review the proposed changes: an update can change other dependencies, and removing
a package can remove packages that require it. Run the relevant code afterward.
Install Conda dependencies before adding packages with pip, and record both in
the project specification. Use the manager that installed a package to remove it.

## Record and recreate an environment

Record the Conda packages you explicitly requested:

```sh
conda env export -n design-test --from-history > design-test.yml
```

For a fuller snapshot of installed versions, omitting build strings:

```sh
conda env export -n design-test --no-builds > design-test-resolved.yml
```

A history export expresses requested Conda dependencies; it does not record all
packages added with pip. A resolved snapshot includes more installed dependencies
but can still contain packages specific to one operating system. Review the file,
including any local `prefix:` path, before sharing it. The `>` operator replaces
an existing file of the same name.

Recreate the exported specification under a new name:

```sh
conda env create -n design-copy -f design-test.yml
```

## Delete an environment

Leave the environment being removed, then delete it by name:

```sh
conda deactivate
conda env remove -n design-test
conda env list
```

Check the target name before confirming. This removes the environment's interpreter
and packages; project files stored elsewhere remain. Keep source files outside
environment directories and retain `base` for Conda itself.

## Quick diagnosis

| Symptom | First check |
| --- | --- |
| `conda` is not found | Follow the [installation and initialization checks](README.md#2-install-and-initialize-conda). |
| Wrong Python or missing imports | Activate the intended environment and repeat the [interpreter checks](README.md#4-verify-the-interpreter-and-imports). |
| Environment file not found | Check the working directory and the path supplied after `-f`. |
| Environment already exists | Inspect it with `conda list -n NAME`; activate or update it, or choose a new name. |
| Dependencies cannot be resolved | Read the conflicting requirements; check Python version, package versions, and channels. |
| A shell command causes a Python syntax error | Enter `exit()` at the `>>>` prompt, then run the command in the terminal. |
