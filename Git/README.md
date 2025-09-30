# Git

## General

`git commit --amend` - Add to previous commit, requires force push
`git pull --rebase origin master` - Rebase on upstream master, requires force push

## New Machine Setup

```bash
# Set global config
$ git config --global user.name "Alex Derr"
$ git config --global user.email myEmail@email.com 

# HTTPS generally works, but can use SSH
# SSH Setup
$ ssh-keygen -o
# Copy output, add it as SSH key in git.
# Clone with SSH
$ git clone <ssh-clone-url>
```