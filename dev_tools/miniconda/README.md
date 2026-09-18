# Miniconda

Miniconda installs Conda, which manages isolated Python environments. Each
environment has its own interpreter and packages. This guide creates the `acd`
environment from the `environment.yml` file in the local tutorial repository.

**Command reference:** [Conda cheat sheet](conda_cheat_sheet.md) — environment
management, package versions, dependency files, and troubleshooting.

**Prerequisite:** clone the tutorial repository with GitHub Desktop and locate
its `environment.yml` file.
If Conda is already installed, verify it with `conda --version` and continue at
[Create the environment](#3-create-the-environment).

**Contents:** [Installation](#1-select-the-installer) · [Create acd](#3-create-the-environment)
· [Verification](#4-verify-the-interpreter-and-imports)

## 1. Select the installer

Use the [Miniconda installation documentation](https://www.anaconda.com/docs/getting-started/installation)
to choose an installer, or obtain it from the official
[Miniconda installer archive](https://repo.anaconda.com/miniconda/).

Choose the build for your operating system and processor. On macOS, **Apple menu →
About This Mac** identifies Apple silicon or Intel. On Windows, **Settings →
System → About** lists the system type.

| System | Installer |
| --- | --- |
| Windows with an Intel or AMD 64-bit processor | Windows `x86_64` executable (`.exe`). |
| Mac with Apple silicon | macOS `arm64` shell installer (`.sh`). |
| Mac with an Intel processor | macOS `x86_64` shell installer (`.sh`) from the archive. |

The last Miniconda series with Intel Mac installers is 25.7; the
[release notes](https://www.anaconda.com/docs/getting-started/miniconda/release/25.x)
identify the available builds. For another architecture, check the official
installation documentation for a compatible build.

The Python version bundled with the Miniconda installer belongs to its `base`
environment. The Python version for `acd` is selected separately by `environment.yml`.

## 2. Install and initialize Conda

### Windows

1. Run the `.exe` installer and review its license terms.
2. Choose **Just Me** and a local installation directory. Record that directory;
   it identifies the Conda installation if you need to locate it later.
3. Leave **Add Miniconda to PATH** unchecked. Use the configured prompt below
   instead of manually adding the installation to the system path.
4. Complete the installation, then open **Anaconda Prompt** from the Start menu.
5. Verify the installation:

   ```bat
   conda --version
   conda info --base
   ```

The first command prints the Conda version; the second prints its installation
folder. To enable Conda in ordinary Command Prompt terminals as well, run:

```bat
conda init cmd.exe
```

Close and reopen Command Prompt after initialization. Continue using Anaconda
Prompt for the remaining steps in this guide.

### macOS

1. Open **Terminal**.
2. Type `bash` followed by a space, drag the downloaded Miniconda `.sh` file into
   the Terminal window, and press Return. Dragging inserts its actual file path.
3. Read the installer prompts and license terms. Accept the proposed installation
   location or choose a local location, and record the path.
4. When asked whether to initialize Conda for your shell, choose **yes**.
5. Close Terminal and open a new window, then run:

   ```sh
   conda --version
   conda info --base
   ```

If the installation succeeded but `conda` is not found, initialize the shell using
the executable in the installation directory. For the usual `~/miniconda3`
location and the macOS default Zsh shell:

```sh
~/miniconda3/bin/conda init zsh
```

Use the recorded installation path if yours differs, then close and reopen
Terminal. For Bash, use `init bash` instead. You can check the configured login
shell with `echo $SHELL`.

## 3. Create the environment

Open Anaconda Prompt on Windows or Terminal on macOS. Change to the cloned
repository folder. Replace the example path with the actual local path from
GitHub Desktop, keeping the quotation marks.

**Windows**

```bat
cd /d "C:\path\to\ACD-Tutorials"
dir environment.yml
```

**macOS**

```sh
cd "/path/to/ACD-Tutorials"
ls environment.yml
```

If the file is listed, create the environment:

```sh
conda env create -f environment.yml
```

Wait for Conda to resolve and install the dependencies. This is a one-time step.
Then activate the environment:

```sh
conda activate acd
```

The environment contains Python, NumPy, pandas, Matplotlib, openpyxl,
scikit-image, and Seaborn. Installation is defined by `environment.yml`; separate
package-by-package installation is unnecessary.

If `acd` already exists, activate it and perform the checks below. If it needs
to be brought into line with the environment file, use the
[environment update reference](conda_cheat_sheet.md#update-or-remove-packages).

## 4. Verify the interpreter and imports

Run these commands in the activated terminal:

```sh
python --version
python -c "import sys; print(sys.executable)"
python -c "import numpy, pandas, matplotlib, openpyxl, skimage, seaborn; print('Ready!')"
```

The expected Python version is `3.9.10`. The executable path should point inside
the `acd` environment, and the import check should print `Ready!` without an error.

From the repository folder, also run:

```sh
python Week00/tutorial/hello_world.py
```

Expected output:

```text
Hello ACD!
```

These checks establish that the interpreter and dependencies work before an editor
is introduced. Keep the executable path available for the VS Code configuration.

## After setup

Use the [Conda cheat sheet](conda_cheat_sheet.md) when creating other environments,
adding packages, specifying versions, exporting dependencies, or removing an
experiment. For an error, start with its [diagnosis table](conda_cheat_sheet.md#quick-diagnosis).
