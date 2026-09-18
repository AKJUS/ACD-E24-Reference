# Development tools

The working environment consists of three components: GitHub Desktop manages the
source files and their history, Miniconda manages Python and its dependencies, and
VS Code provides the editor and execution interface. These guides also cover
package installation, version control, and technical documentation as references
for everyday work.

## Installation sequence

| Step | Walkthrough | Result |
| --- | --- | --- |
| 1 | [GitHub Desktop](github_desktop/README.md) | Git identity configured and the tutorial repository cloned locally. |
| 2 | [Miniconda](miniconda/README.md) | The `acd` environment created from `environment.yml` and its imports verified. |
| 3 | [Visual Studio Code](vscode/README.md) | Microsoft's Python extension installed and both the editor and terminal using `acd`. |

Complete the environment configuration before configuring the editor. If a tool
is already installed, proceed to its configuration and verification sections.

## Working references

| Tool | Overview or walkthrough | Cheat sheet |
| --- | --- | --- |
| Git | [Repository concepts](git/README.md) | [Concepts and commands](git/git_cheat_sheet.md) |
| Markdown | [Technical documentation](markdown/README.md) | [Syntax and examples](markdown/markdown_cheat_sheet.md) |
| Miniconda | [Installation and initial setup](miniconda/README.md) | [Conda commands](miniconda/conda_cheat_sheet.md) |
| pip | [Package reference overview](pip/README.md) | [pip commands](pip/pip_cheat_sheet.md) |

## Common operations

| Task | Reference |
| --- | --- |
| Create and configure a GitHub account | [GitHub account setup](github_desktop/README.md#github-account) |
| Create, clone, export, or delete an environment | [Conda environment management](miniconda/conda_cheat_sheet.md) |
| Choose a Python or package version | [Conda version constraints](miniconda/conda_cheat_sheet.md#install-packages-and-select-versions) |
| Add a Python library or pin its version | [pip](pip/README.md) |
| Record dependencies for another installation | [Requirements and environment files](pip/pip_cheat_sheet.md#use-requirements-files) |
| Change the interpreter or debug a script | [VS Code](vscode/README.md) |
| Review, commit, branch, or synchronize changes | [GitHub Desktop](github_desktop/README.md#everyday-version-control) |
