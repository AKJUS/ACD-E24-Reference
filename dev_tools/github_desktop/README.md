# GitHub Desktop

GitHub Desktop provides a graphical interface to Git. This walkthrough covers
installation, authentication, commit identity, cloning, and repository updates.
The result is a local repository ready for Python environment configuration.

**Contents:** [GitHub account](#github-account) · [Installation](#1-install-the-application) · [Git configuration](#2-configure-git)
· [Clone](#3-clone-the-tutorial-repository) · [Updates](#5-receive-updates-and-preserve-local-work)
· [Commits and branches](#everyday-version-control) · [Troubleshooting](#troubleshooting)

## GitHub account

GitHub is the hosting service; GitHub Desktop is the application connecting your
local repositories to it. Use an existing personal GitHub account if you have one.

### Create an account

1. Open [GitHub sign-up](https://github.com/signup) in a browser.
2. Follow the prompts to create a personal account. Use an email address you can
   access, choose a username, and complete the selected sign-in method.
3. Complete the email verification requested during registration.
4. Sign in and open **Your profile** from the account menu. Confirm the username
   displayed on the profile; it is distinct from your profile's display name and
   the author name configured in Git.

A free personal account is sufficient for the repository operations in this guide.
See [GitHub's account creation documentation](https://docs.github.com/en/account-and-profile/how-tos/account-management/creating-an-account-on-github)
for the current sign-up options.

### Verify and configure the account

Under **Settings → Emails**, check that the intended address is verified. If needed,
use **Resend verification email** and complete verification from the received email.
This page also provides GitHub's private commit email address when email privacy
is enabled; you can select that address when configuring Git below.

GitHub recommends [two-factor authentication](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication).
Configure it under **Settings → Password and authentication**, and retain the
recovery codes in a secure location accessible if the authentication device is lost.

Use this same account when signing into GitHub Desktop. Browser authentication
connects the application to the account; the Git name and email configured later
identify the commits you create.

## 1. Install the application

Download the installer for your operating system from
[GitHub Desktop](https://desktop.github.com/).

### Windows

1. Run the downloaded installer and allow it to finish.
2. Open **GitHub Desktop** from the Start menu if it does not open automatically.
3. Select **Sign in to GitHub.com** and complete authentication in the browser.
4. Return to the application when the browser offers to open GitHub Desktop.

### macOS

1. Open the downloaded archive and move **GitHub Desktop** to **Applications**.
2. Launch it from Applications and confirm the operating system's first-launch prompt.
3. Select **Sign in to GitHub.com**, authenticate in the browser, and return to the application.

GitHub Desktop includes the Git components it needs; a separate command-line Git
installation is not required for this guide.

The official application supports Windows and macOS; this guide uses those
platforms.

## 2. Configure Git

Authentication connects the application to your GitHub account. Git configuration
sets the author information recorded in your commits.

Open the application's settings:

| Windows | macOS |
| --- | --- |
| **File → Options** | **GitHub Desktop → Settings** |

1. Select **Git**.
2. Enter the name you want attached to your commits.
3. Select an email address associated with your GitHub account. A GitHub-provided
   private email address can be used if you prefer not to expose your email in public commits.
4. Save the settings. Under **Default branch**, use `main` for newly created repositories.

This does not rename branches in repositories you clone. Leave the external-editor
setting until VS Code is installed. Then select **Integrations → External Editor →
Visual Studio Code** in these settings.

## 3. Clone the tutorial repository

Cloning downloads both the files and their Git history, and records the original
repository as the remote named `origin`.

1. Choose **File → Clone Repository**.
2. Open the **URL** tab and enter:

   ```text
   https://github.com/AdvancedComputationalDesign-SDU/ACD-Tutorials
   ```

3. Set **Local Path** to a location you can identify easily, such as a `GitHub`
   folder within Documents. The final repository folder should be named `ACD-Tutorials`.
4. Select **Clone** and wait for the operation to finish.
5. Use **Repository → Show in Explorer** on Windows or **Show in Finder** on macOS
   to inspect the local folder.

The folder should contain `README.md`, `environment.yml`, and `Week00`. Keep these
files in the cloned folder; the environment setup uses `environment.yml` from there.
Downloading a ZIP archive does not retain the Git connection used for updates.

## 4. Inspect the repository

| Area | Purpose |
| --- | --- |
| **Current Repository** | Identifies which local repository you are operating on. |
| **Current Branch** | Identifies the active line of development. |
| **Changes** | Shows files that differ from the last commit. |
| **History** | Shows commits and the changes recorded in each one. |
| **Fetch origin** | Checks the remote repository for new commits. |

Immediately after cloning, the Changes list should be empty. Inspect History to
confirm that the downloaded commit history is present.

## 5. Receive updates and preserve local work

Select the repository and its `main` branch, then choose **Fetch origin**. If new
commits are available, choose **Pull origin** to update the local files.

Before pulling, inspect **Changes**. If you have modified an example, preserve
those edits first. For experiments that do not need their own Git history, copy
the complete week folder to a separate working directory. Include any data and
helper files so relative paths continue to resolve. Verify the copy before
replacing or discarding edits in the original.

A separate working copy does not receive updates automatically and needs its own
backup. If you work on a local branch instead, commit your changes there before
switching branches. The [branch workflow](#work-on-a-branch) below explains
how to keep an experiment on its own line of development.

**Discard changes** restores selected files to their committed content. Use it
only after checking that the edits are no longer needed or have been preserved.
If a pull reports conflicting edits or diverged history, inspect the affected
files before choosing how to combine them.

## Everyday version control

### Review and commit changes

Save edited files, then open **Changes** in GitHub Desktop. Select each file to
inspect its diff: added lines, removed lines, and any unintended changes.
Use the checkboxes to select the files or changes that belong in one commit.

Enter a summary describing the change, such as `Correct array-axis order in image
export`, then select **Commit to** the current branch. The commit is stored locally.
If the remote is a repository you can write to, **Push origin** uploads the commit.
Use **Repository → View on GitHub** to inspect the remote result.

Keep generated files, local environments, and other files that do not belong in
version history out of commits. A repository's `.gitignore` specifies which
untracked paths Git should ignore; it does not stop tracking files already committed.

### Create a repository for your own project

Use **File → New Repository**. Choose a name, a local parent directory, and any
appropriate initialization options, such as a README and Python `.gitignore`.
Inspect the path before creating it so the new repository is not accidentally
nested inside another repository.

A new local repository remains on your computer until you publish it. If you
choose **Publish repository**, check the account, repository name, and visibility
before publishing. An existing remote project should be cloned instead.

### Work on a branch

A branch records a separate line of changes within the same repository. Before
switching branches, commit or otherwise preserve unfinished edits.

1. Select **Current Branch → New Branch**.
2. Name the branch for the work, such as `compare-field-functions`.
3. Make and commit the changes on that branch.
4. Compare the branch with the original before deciding whether to merge it.

A branch uses the same working directory; switching branches updates the files
in that directory. It is not an independent backup. Publishing a branch requires
write access to the selected remote repository.

### Inspect history and recover earlier content

Select **History**, choose a commit, and inspect its changed files. For a small
recovery, copy the required earlier content back into the working file, check it,
and record a new commit.

To reverse an entire committed change without deleting its history, right-click
the commit and choose **Revert Changes in Commit**. Review the result, particularly
if later work depends on the reverted change. Reverting can itself require conflict
resolution. Discarding uncommitted work and reverting a commit are different operations.

### Resolve a conflict

A conflict means Git cannot combine the edits automatically. Open the affected
files and inspect both versions. Resolve the text into the intended final result,
remove any conflict markers, save, and verify the code before completing the merge.
Keep a copy of important files if you are uncertain. Choosing one entire side
without reading it can remove valid work from the other side.

## Verification

The application should show your signed-in account, a configured Git name and
email, and the cloned repository. **Fetch origin** should complete successfully,
and `environment.yml` should be visible in the local repository folder.

## Troubleshooting

| Issue | Diagnosis and resolution |
| --- | --- |
| Authentication returns to the browser repeatedly | Check the account signed into the browser, then reopen Desktop and complete its sign-in flow. |
| Cloning reports that the destination already exists | Inspect that folder first. Add an existing valid clone with **File → Add Local Repository**, or select another empty destination. |
| The repository cannot be found | Check the URL and the account's access to the repository. |
| Pull is blocked by local changes | Preserve the files or commit the changes on the appropriate branch before integrating the update. |
| Desktop offers to create a fork when pushing | The account does not have write access to the original repository. Receiving updates requires fetch and pull, not a push. |
