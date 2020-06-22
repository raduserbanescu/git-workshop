# Install Git for Windows

*Setup Guide and verification checklist*

## Setup

**Tested on:** Git for Windows 2.27.0.windows.1

**Note:** If you are installing a newer version that has additional steps, leave those new steps at their default values.

### Step 0: Download

Download the installation package from the [Git official website][git-scm website].

### Step 1: License

If you are updating, *uncheck* the **"Only show new options"** checkbox in order to see all the installation steps.

![License][setup step 1]

### Step 2: Components

Leave the default components as shown below.

![Components][setup step 2]

### Step 3: Default Editor

If you leave the default option, Git will use the Bash default editor (based on the `EDITOR` environment variable), which is Vim. Vim can be hard to use and unintuitive compared to modern editors.

The Git `core.editor` option will remain unset, but this can be modified later on in your personal configuration.

![Default Editor][setup step 3 a]

**Recommended:** Select here one of your favorite editors which you already have installed on your system.

![Default Editor][setup step 3 b]

### Step 4: PATH environment

**Recommended:** Select the option **"Git from the command line and also from 3rd-party software"**.

![PATH environment][setup step 4]

### Step 5: HTTPS connections

Leave the default option **"Use the OpenSSL library"**.

![HTTPS][setup step 5]

### Step 6: Line endings

**Recommended:** Select the option **"Checkout as-is, commit Unix-style line endings"**. With this option we ensure that we always have `LF` line endings inside the repository.

Don't overcomplicate things by forcing Git to convert line endings. All modern Windows code editors work with Unix-style `LF` line endings. Also, there are development tools that rely on `LF` line endings to work properly (npm scripts, linters, etc...).

**TIP:** If you use file types that *explicitly require* `CRLF` line endings, specify them in a [`.gitattributes`][git attributes] file.

Reference reading:

- <https://jessitron.com/2019/11/11/line-endings-in-git/>
- <https://markoskon.com/line-endings-in-vscode-with-git-and-eslint/>

![Line endings][setup step 6]

### Step 7: Terminal emulator

Leave the default option as shown below.

![Terminal emulator][setup step 7]

### Step 8: Default behavior of `git pull`

Leave the default option as shown below.

![Default git pull][setup step 8]

### Step 9: Extra features

Leave the default options as shown below.

![Extra features][setup step 9]

### Step 10: Experimental features

Don't select any experimental feature, as shown below.

![Experimental features][setup step 10]

### Step 11: Finish the setup

Congratulations! You've completed the installation. Now let's verify that everything works correctly.

![Finish][setup step 11]

## Verify the installation

In the Windows context menu you should see two new options, one of which is **"Git Bash Here"**.

![Context Menu][verify step 1] ![Git Bash][verify step 2]

Check that the `git` command was added to the [PATH environment variable][]. This way external tools can use our installed Git version.

Run `git --version` in CMD and PowerShell.

![CMD][verify step 3] ![PowerShell][verify step 4]

<!-- Definitions -->

[git-scm website]: https://git-scm.com/
[git attributes]: https://git-scm.com/book/en/v2/Customizing-Git-Git-Attributes
[path environment variable]: https://en.wikipedia.org/wiki/PATH_(variable)

[setup step 1]: images/Setup-Step_01-License.png
[setup step 2]: images/Setup-Step_02-Components.png
[setup step 3 a]: images/Setup-Step_03_A-Default_Editor.png
[setup step 3 b]: images/Setup-Step_03_B-Default_Editor.png
[setup step 4]: images/Setup-Step_04-PATH_environment.png
[setup step 5]: images/Setup-Step_05-HTTPS.png
[setup step 6]: images/Setup-Step_06-Line_endings.png
[setup step 7]: images/Setup-Step_07-Terminal_emulator.png
[setup step 8]: images/Setup-Step_08-Default_git_pull.png
[setup step 9]: images/Setup-Step_09-Extra_features.png
[setup step 10]: images/Setup-Step_10-Experimental_features.png
[setup step 11]: images/Setup-Step_11-Finish.png

[verify step 1]: images/Verify-Step_01-Context_Menu.png
[verify step 2]: images/Verify-Step_02-Git_Bash.png
[verify step 3]: images/Verify-Step_03-CMD.png
[verify step 4]: images/Verify-Step_04-PowerShell.png
