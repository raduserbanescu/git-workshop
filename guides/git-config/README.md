# Git Configuration

*Some recommended settings for a good starting point*

Git comes with a tool called [`git config`][git config] that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

1. **System-wide** in the `/etc/gitconfig` file, which contains settings that are applied to every user on the system and all of their repositories. Pass the `--system` option to read and write to this file. (Because this is a system configuration file, you would need administrative or superuser privilege to make changes to it.)
2. **User specific** in the `~/.gitconfig` file, which contains your personal settings and these affect all of the repositories you work with on your system. Pass the `--global` option to read and write to this file.
3. **Single repository specific** in the `.git/config` file of whatever repository you’re currently using. Pass the `--local` option to read and write to this file, but this is in fact the default. (Unsurprisingly, you need to be located somewhere in a Git repository for this option to work properly.)

Each level overrides values in the previous level: *Local* > *Global* > *System*

You can view all of your settings and where they are coming from using:

```console
$ git config --list --show-origin
```

or

```console
$ git config --list --show-scope
```

## Basic Setup

You should go through these settings when you first start using Git and save them in your *user specific* configuration file. This way you will just have to copy your `~/.gitconfig` file when you move to another system.

### Identity

This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating.

Also, your email address is used to link the commits you push to an online Git service with your user account (example: GitHub).

```console
$ git config --global user.name "YOUR NAME"

$ git config --global user.email "your_email@example.com"
```

**TIP:** If you want to override your identity just for specific projects, you can run the commands without the `--global` option when you’re inside that project.

### Editor

Next we will configure the default text editor that will be used when Git needs you to type in a message.

If not configured, Git uses your system’s default editor (based on the `EDITOR` environment variable), or else falls back to the Vim editor.

```console
$ git config --global core.editor "COMMAND OPTIONS"
```

Some examples:

```console
# Atom
$ git config --global core.editor "atom --wait"

# Notepad++
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

# Visual Studio Code
$ git config --global core.editor "code --wait"
```

**TIP:** [Specific instructions for how to set up your favorite editor with Git][core.editor list]

### Line endings

With the option below we ensure that we always have `LF` line endings inside the repository. Git will not perform any conversion when checking out text files. When committing text files, `CRLF` will be converted to `LF`.

Don't overcomplicate things by forcing Git to convert line endings. All modern code editors work with Unix-style `LF` line endings. Also, there are development tools that rely on `LF` line endings to work properly (npm scripts, linters, etc...).

```console
$ git config --global core.autocrlf input
```

**TIP:** If you use file types that *explicitly require* `CRLF` line endings, specify them in a [`.gitattributes`][git attributes] file.

Reference reading:

- <https://jessitron.com/2019/11/11/line-endings-in-git/>
- <https://markoskon.com/line-endings-in-vscode-with-git-and-eslint/>

### Others

Some sane defaults to get you going until you start to learn more about Git.

```console
$ git config --global pull.ff only

$ git config --global push.default simple
```

Reference reading:

- <https://blog.sffc.xyz/post/185195398930/why-you-should-use-git-pull-ff-only>
- <https://news.ycombinator.com/item?id=14047241>

## Checking your settings

You can check what Git thinks a specific key’s value is by typing `git config SECTION.KEY`

Examples:

```console
$ git config user.name
YOUR NAME

$ git config user.email
your_email@example.com

$ git config core.autocrlf
input
```

You can also use the `--show-origin` or `--show-scope` options in order for Git to tell you from which configuration file the value is coming from.

Examples:

```console
$ git config --show-origin user.name
file:~/.gitconfig   YOUR NAME

$ git config --show-scope user.email
global  your_email@example.com
```

## Troubleshooting

- [Why are my commits linked to the wrong user?][]
- [Getting started with Git and GitHub][]

## References

- <https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup>
- <https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration>
- <https://git-scm.com/docs/git-config>

<!-- Definitions -->

[git config]: https://git-scm.com/docs/git-config
[core.editor list]: https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config#_core_editor
[git attributes]: https://git-scm.com/book/en/v2/Customizing-Git-Git-Attributes

[why are my commits linked to the wrong user?]: https://help.github.com/en/github/committing-changes-to-your-project/why-are-my-commits-linked-to-the-wrong-user
[getting started with git and github]: https://help.github.com/en/github/using-git/getting-started-with-git-and-github
