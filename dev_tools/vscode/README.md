# Visual Studio Code

VS Code provides the editor, terminal, and debugging interface. Microsoft's Python
extension connects those tools to an existing Python interpreter. This guide
configures it to use the `acd` Conda environment.

**Prerequisite:** create and activate the `acd` Conda environment, then verify
that Python and its required libraries run successfully in a terminal.

**Contents:** [Installation](#1-install-vs-code) · [Python extension](#2-install-microsofts-python-extension)
· [Interpreter](#4-select-the-conda-interpreter) · [Terminal](#5-configure-the-terminal-and-verify-execution)
· [Editor and debugger](#editor-and-debugging-basics) · [Troubleshooting](#troubleshooting)

## 1. Install VS Code

Download **Visual Studio Code** from the
[official download page](https://code.visualstudio.com/download), selecting the
build for your operating system and processor.

### Windows

1. Run the User Installer and complete the installation for your account.
2. Keep the option to add VS Code to PATH enabled if you want to open folders with `code` from a terminal.
3. Launch **Visual Studio Code** from the Start menu.

### macOS

1. Extract the downloaded archive and move **Visual Studio Code.app** to **Applications**.
2. Open it from Applications.
3. To enable the optional `code` terminal command, open the Command Palette and run
   **Shell Command: Install 'code' command in PATH**. Reopen the terminal afterward.

## 2. Install Microsoft's Python extension

1. Open **Extensions** from the Activity Bar: **Ctrl+Shift+X** on Windows or **Cmd+Shift+X** on macOS.
2. Search for `ms-python.python`.
3. Select **Python**, published by **Microsoft**, and choose **Install**.
4. Allow any required supporting extensions to finish installing. Reload VS Code if prompted.

The extension provides Python execution and editor support. The Python interpreter
and scientific libraries come from Conda. A separate Python installation, Code
Runner extension, or Jupyter installation is not required for these `.py` files.

## 3. Open the project folder

Use **File → Open Folder** to open the cloned `ACD-Tutorials` directory. The Explorer
should show `README.md`, `environment.yml`, and `Week00`.

Open the folder itself, rather than only an individual Python file. This gives the
editor a project context and makes relative paths and interpreter selection easier
to manage. If VS Code asks about Workspace Trust, review the folder's source and
trust it when you are satisfied it is the repository you intended to open.

## 4. Select the Conda interpreter

1. Open `Week00/tutorial/hello_world.py` in the editor.
2. Open the Command Palette with **Ctrl+Shift+P** on Windows or **Cmd+Shift+P** on macOS.
3. Run **Python: Select Interpreter**.
4. Select the entry for **acd**. Check its environment name and executable path;
   do not select `base` or a system Python interpreter.
5. With a Python file active, inspect the interpreter indicator in the status bar.

Interpreter selection applies to the current project. Check it again when you
open a different folder.

### If acd is not listed

In Anaconda Prompt or Terminal, run:

```sh
conda activate acd
python -c "import sys; print(sys.executable)"
```

Copy the resulting executable path. Return to **Python: Select Interpreter** and
choose **Enter interpreter path…**, then select that executable. On Windows it
ends in `python.exe`; on macOS it is normally `bin/python` inside the environment.

If the **Python Environments** extension is available, its refresh command can
rescan the installed environments. Selecting the executable directly also works
when automatic discovery does not find your Conda installation.

## 5. Configure the terminal and verify execution

An existing terminal may retain an earlier environment even after changing the
editor's interpreter. Close old terminal sessions using the terminal panel's
trash icon, then create a new one with **Terminal → New Terminal**.

On Windows, this walkthrough uses **Command Prompt**, initialized in the Miniconda
guide. To choose it, run **Terminal: Select Default Profile → Command Prompt** from
the Command Palette, then create a new terminal. On macOS, use the shell initialized
during the Conda installation, normally Zsh.

The Python extension should activate the selected environment in a new terminal.
Verify rather than relying only on the prompt label:

```sh
python -c "import sys; print(sys.executable)"
python --version
```

The executable should match the `acd` path selected above, and the Python version
should be `3.9.10`. If the terminal is using another interpreter, run
`conda activate acd` and repeat the checks.

From the repository folder, verify the dependencies and run the example:

```sh
python -c "import numpy, pandas, matplotlib, openpyxl, skimage, seaborn; print('Ready!')"
python Week00/tutorial/hello_world.py
```

The checks should print `Ready!` and `Hello ACD!`. Then open `hello_world.py` and
run **Python: Run Python File in Terminal** from the Command Palette. This should
produce the same greeting through the editor's Python command.

### Running complete files and selected sections

Save a file before running it. Use **Python: Run Python File in Terminal** for a
complete script. To evaluate a section, select complete statements and use
**Python: Run Selection/Line in Python Terminal**. Execute the imports and any
file-location setup before the section that depends on them.

Selected code runs in an interactive session whose variables persist. Start a
fresh Python session when checking whether a script runs independently. Close a
plot window when a whole-file run waits for it before continuing.

## 6. Connect GitHub Desktop to VS Code

Now that VS Code is installed, set it as GitHub Desktop's external editor:

1. In GitHub Desktop, open **File → Options** on Windows or **GitHub Desktop → Settings** on macOS.
2. Select **Integrations**.
3. Choose **Visual Studio Code** under **External Editor** and save.
4. Select a repository and use **Repository → Open in Visual Studio Code**.

Check the selected Python interpreter when the folder opens. The Git application
chooses the folder; VS Code's project configuration chooses its interpreter.

## Editor and debugging basics

### Navigate and inspect

| Operation | Windows | macOS |
| --- | --- | --- |
| Open a file by name | **Ctrl+P** | **Cmd+P** |
| Find within the current file | **Ctrl+F** | **Cmd+F** |
| Search across the open folder | **Ctrl+Shift+F** | **Cmd+Shift+F** |
| Open the Command Palette | **Ctrl+Shift+P** | **Cmd+Shift+P** |
| Save the current file | **Ctrl+S** | **Cmd+S** |

Use **View → Problems** to inspect diagnostics. Hover over a symbol for information
and use its context menu to navigate to a definition. Treat editor diagnostics as
useful evidence, then verify behavior by executing the code.

### Inspect the working directory

The interpreter and the working directory are independent settings. A correct
interpreter can still fail to find a file when execution starts in the wrong folder.
In the integrated terminal, inspect both:

```sh
python -c "import sys, os; print(sys.executable); print(os.getcwd())"
```

Use `cd` to change the terminal's directory. In a script, paths relative to
`__file__` refer to its file location; paths relative to the working directory
refer to where the process started. Follow each script's supplied path setup when
running only selected sections.

### Debug a calculation

1. Open a saved Python file and click in the left gutter beside a statement to set a breakpoint.
2. Open **Run and Debug** and start a Python debugging session. If prompted, choose **Python Debugger** and **Python File**; install Microsoft's Python Debugger extension if requested.
3. When execution pauses, inspect **Variables** and hover over expressions in the editor.
4. Use **Step Over** to execute the next statement, **Step Into** to enter a function, and **Continue** to run to the next breakpoint.
5. Use **Stop** to end the session. Remove a breakpoint by clicking it again.

A breakpoint pauses before the marked statement executes. Inspect a value before
and after the step to understand how an operation changes program state. The
Debug Console can evaluate expressions in the paused context; distinguish
inspection from expressions that modify that state.

### Manage extensions and project settings

Use **Extensions** to inspect installed extensions and their publishers. Settings
can apply to your user account or only to the current workspace. Use workspace
settings for project-specific behavior and user settings for general editor
preferences.

When you add a library with Conda or `python -m pip`, install it in the
environment selected for this project. An editor extension is not a
Python library: installing the Python extension does not install NumPy or other
project dependencies.

## Troubleshooting

| Issue | Diagnosis and resolution |
| --- | --- |
| `Python: Select Interpreter` is unavailable | Confirm that Microsoft's Python extension is installed and enabled, open a `.py` file, and reload VS Code. |
| `acd` is missing from the selection list | Confirm it exists with `conda env list`, then select its executable using **Enter interpreter path…**. |
| The editor shows acd but the terminal uses another Python | Close the existing terminal, create a new one, and compare `sys.executable` with the selected interpreter. |
| Conda activation fails in the Windows terminal | Use the initialized Command Prompt profile. Run `conda init cmd.exe` from Anaconda Prompt if needed, restart VS Code, and create a new terminal. |
| PowerShell reports that profile scripts are blocked | Use Command Prompt for this workflow. Changing the system's execution policy is not necessary. |
| `ModuleNotFoundError` | Verify that the command is using `acd`. Check the imports in Anaconda Prompt or Terminal before changing package installations. |
| A data file is missing | Open the correct project folder and retain the full example directory, including its data. For selected sections, run the supplied path setup first. |
