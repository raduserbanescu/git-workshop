# Setup multiple SSH keys

*Guide on how to setup Git to use one or multiple SSH keys*

These days there are a lot of online services that offer Git hosting (GitHub, GitLab, Bitbucket, etc...) and each one requires a set of SSH keys. Below, I will show you a process to easily manage one or multiple SSH keys.

## Before we begin

**Attention Windows users:** In this guide when referring to a *Terminal*, please open the *Git Bash* from the context menu. Also, the `~` shorthand refers to your [Home directory][] (example: `C:\Users\YOUR_USER`).

### Check for existing SSH keys

If you already used Git, you might have an existing SSH key.

Go to your `~/.ssh` directory and check if you have a pair of files named something like `id_dsa` or `id_rsa` and a matching file with a `.pub` extension. The `.pub` file is your public key, and the other file is the corresponding private key.

If you have `id_dsa` keys, it's best if you delete them now and go through the next steps to generate a new SSH key. These use a very old standard.

---

If you have a single `id_rsa` pair I would suggest you do this:

Find out for what service you use them by going to an existing Git project on your computer and running this command:

```console
$ git remote -v
origin  git@github.com:raduserbanescu/git-workshop.git (fetch)
origin  git@github.com:raduserbanescu/git-workshop.git (push)
```

Remember the *username* (example: `git` from above) and the *hostname* (example: `github.com` from above).

Rename the SSH keys pair to something more self explanatory like for example `id_rsa_personal_github` and `id_rsa_personal_github.pub`.

Follow along with the next steps in this guide, but skip the SSH key generation.

## Setup

Go through these steps each time you need a new SSH key for a Git online service that you use.

### Step 1: Generate a new SSH key

Open a Terminal and run these commands.

```console
$ cd ~/.ssh
```

Use your email address.

```console
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Generating public/private rsa key pair.
```

Name your key, don't use the default name.

```console
Enter file in which to save the key (~/.ssh/id_rsa): id_rsa_SOMETHING_HERE
```

Enter your passphrase. Optional for increased security.

```console
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

The SSH key was generated.

```console
Your identification has been saved in ....................
Your public key has been saved in ....................
The key fingerprint is:
....................
The key's randomart image is:
....................
```

### Step 2: Create a SSH `config` file

If you do not already have a `~/.ssh/config` file, create an empty file now.

```console
$ touch ~/.ssh/config
```

### Step 3: Add the new key to the SSH `config` file

For each new key you generate, you need to add a new block.

Template:

```ssh_config
# Description comment
Host example.com
	User git
	HostName example.com
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_SOMETHING_HERE
	AddKeysToAgent yes
```

Example:

```ssh_config
# Personal GitHub
Host github.com
	User git
	HostName github.com
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_personal_github
	AddKeysToAgent yes
```

### Step 4: Add the new SSH key to your online account

Copy the contents of the `.pub` file (example: `id_rsa_personal_github.pub`).

Simplest method: Go in the `~/.ssh` directory, open the `.pub` file with your favorite text editor, Select All, Copy.

Add it to your online account, depending on which service you use:

- [GitHub account][add ssh key github]
- [GitLab account][add ssh key gitlab]
- [Bitbucket account][add ssh key bitbucket]

### Step 5: Test your SSH connection

Run this command, using your service hostname.

```console
$ ssh -T git@github.com
```

If this is the first time you connect to that service, you will get a warning. The SSH client asks you if it can trust the public key of the service.

```console
The authenticity of host '..........' can't be established.
RSA key fingerprint is ....................
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type `yes` to confirm. The SSH client adds the service to the list of trusted hosts inside the file `~/.ssh/known_hosts`.

```console
Warning: Permanently added '..........' (RSA) to the list of known hosts.
```

If you have a passphrase or you didn't enter it before, you will be prompted now. Your `ssh-agent` should remember it for a period of time.

```console
Enter passphrase for key '~/.ssh/id_rsa_SOMETHING_HERE':
```

If everything is setup correctly, you should see a welcome message containing *your username*.

```console
Hi raduserbanescu! You've successfully authenticated, but GitHub does not provide shell access.
```

## Troubleshooting

- [Working with SSH key passphrases][]
- [Troubleshooting SSH][]

## References

- <https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key>
- <https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh>
- <https://docs.gitlab.com/ee/ssh/>
- <https://kamarada.github.io/en/2019/07/14/using-git-with-ssh-keys/>
- <https://www.ssh.com/ssh/>
- <https://man.openbsd.org/ssh_config>

<!-- Definitions -->

[home directory]: https://en.wikipedia.org/wiki/Home_directory

[add ssh key github]: https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account
[add ssh key gitlab]: https://docs.gitlab.com/ee/ssh/#adding-an-ssh-key-to-your-gitlab-account
[add ssh key bitbucket]: https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/

[working with ssh key passphrases]: https://help.github.com/en/github/authenticating-to-github/working-with-ssh-key-passphrases
[troubleshooting ssh]: https://help.github.com/en/github/authenticating-to-github/troubleshooting-ssh
