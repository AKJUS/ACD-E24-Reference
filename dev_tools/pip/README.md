# pip

pip is Python's package installer. It downloads libraries, usually from the Python
Package Index (PyPI), and installs them into an existing Python environment.
This folder covers adding dependencies, selecting versions, checking installations,
and recording the packages a project needs.

## Essential commands

With the intended environment active, check the interpreter and install a library.
NumPy is an example; substitute the package required by your project.

```sh
python -c "import sys; print(sys.executable)"
python -m pip --version
python -m pip install numpy
python -m pip check
```

Use `python -m pip` to target that interpreter. For a Conda environment, install
Conda dependencies first and use pip for the remaining packages. See the
[combined workflow](pip_cheat_sheet.md#combine-conda-and-pip) when using both.

## Reference

- [Command cheat sheet](pip_cheat_sheet.md) — Installation, inspection, updates, removal, and troubleshooting.
- [Version constraints](pip_cheat_sheet.md#specify-versions) — Exact releases, minimum versions, and ranges.
- [Requirements files](pip_cheat_sheet.md#use-requirements-files) — Dependency lists and installed-version snapshots.
- [Combined Conda and pip specification](pip_cheat_sheet.md#combine-conda-and-pip) — Recording both package managers in an environment file.
