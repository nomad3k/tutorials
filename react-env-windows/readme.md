# Setting up Windows to Develop React

This document is copyright 2021 Unchain Life Ltd.

## Table of Contents <!-- omit in toc -->
- [Setting up Windows to Develop React](#setting-up-windows-to-develop-react)
- [Configuring Windows](#configuring-windows)
  - [Windows Terminal](#windows-terminal)
  - [WSL2 (Windows Sub-System for Linux with Ubuntu)](#wsl2-windows-sub-system-for-linux-with-ubuntu)
  - [Visual Studio Code](#visual-studio-code)
- [Configuring WSL](#configuring-wsl)
  - [Git](#git)
  - [NVM](#nvm)
- [Node Project](#node-project)
  - [Lerna](#lerna)
  - [NextJS](#nextjs)
  - [React Components](#react-components)
    - [Atomic UI Design](#atomic-ui-design)
    - [NPM Package Components](#npm-package-components)

# Configuring Windows

## Windows Terminal

You can install Windows Terminal from the Microsoft App Store.  Once installed you can find instructions for accessing your WSL prompt online.

## WSL2 (Windows Sub-System for Linux with Ubuntu)

WSL allows you to run Linux bash inside Windows.  Most tutorials you see online for node/react will be written on an *ix operating system, whether that's Linux or a Mac.  Running WSL allows you to use those same instructions.  Also, a number of tools are available from the CLI in linux, a while windows CLI versions do exist for some they do not exist for all.  e.g. Kubernetes, Docker, Azure, AWS, etc.

The instructions for installing WSL2 and the version of Ubuntu change, so google them for detailed instructions.  Anything written here will go out of date rapidly.

## Visual Studio Code

Visual Studio Code is a lightweight editor that allow you to edit and debug React and Node applications.  It integrates with WSL, allowing you to access files within the Linux partition.

1. Install: Google the instructions.
2. Start from inside WSL: `code .`

# Configuring WSL

## Git

You should install git from the command line, as this can be used to update code manually or as part of scripts.  Mastering the git cli is an important skill, and is far better than using GUIs.

1. Install: `sudo apt install git-all`
2. Configure SSH key: Google this.  It is something like this:
    1. Create a new set of keys: `ssh-keygen -C user@example.org` by default it will generate `id_rsa` and `id_rsa.pub` files.
    2. Copy the contents of `~/.ssh/<your-file-name>.pub` file into your account (github, bitbucket, azure devops)
    3. Optionally use a `~/.ssh/config` to support multiple or non `id_rsa` keys:
        ```
        Host ssh.dev.azure.com
            User git
            PreferredAuthentications publickey
            IdentityFile ~/.ssh/<your-azure-file>
        Host github.com
            User git
            PreferredAuthentications publickey
            IdentityFile ~/.ssh/<your-github-file>
        Host bitbucket.org
            User git
            PreferredAuthentications publickey
            IdentityFile ~/.ssh/<your-bitbucket-file>
        ```
3. Use Git
4. Configure a prompt by adding this to your `~/.bash_profile`, `~/.bashrc` or `~/.zshrc` (depending on which shell you decided to use):
   ```
    parse_git_branch() {
        git branch 2> /dev/null \
            | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
    }

    parse_git_status() {
        git status -s 2> /dev/null \
            | sed -Ee 's/[ ]*([ACDMRU?]+).*/\1/' \
            | sort \
            | uniq -c \
            | sort \
            | tr -d '\n' \
            | sed -Ee 's/[ ]*([0-9]+)[ ]+([ACDMRU?]+)[ ]*/ \2:\1/g'
    }

    export PS1="\[\e[0;33m\][\u] \[\e[32m\]\w/\[\e[35m\]\$(parse_git_branch)\[\e[36m\]\$(parse_git_status) \[\e[0m\]\n$ "
    ```
5. You should now have a nice bash prompt that gives you information about the status of files in your current directory.

## NVM

The "Node Version Manager" allows you to run multiple versions of node on the same computer.  This is important, as you will end up supporting many products over time.  Requiring all versions of your code to run on the same version of node will cause you a lot of upgrade pain, leaving you in an all-or-nothing situation.  Using NVM you can upgrade products individually, as needed.  Also, you will have no control over third party products you use.

1. Install instructions: https://github.com/nvm-sh/nvm#installing-and-updating
2. Installing Node Stable version: `nvm install stable`
3. Restart Terminal
4. Check noed is installed: `node -v`

# Node Project

## Lerna

Lerna is a handy tool that allows you to manage multiple node projects from within a single handy directory.

## NextJS

See https://nextjs.org/

## React Components

### Atomic UI Design

See https://atomicdesign.bradfrost.com/chapter-2/

### NPM Package Components

Hosting components inside a separate NPM package can be very complicated, and should only be attempted once you are familiar with the inner workings of React and Node.
