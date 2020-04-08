+++
categories = ["shortcuts and commands"]
date = "2020-04-07"
description = "Using Git with the command line."
title = "Git Cheat Sheet Volume II"
type = "post"

+++

Just can't Git enough? Below are a list of useful Git commands to reference once you've memorized the basics.

## Setup:

| Command | Description |
|---------|-------------|
git config -global user.name "First Last" | Set a name
git config --global color.ui auto| automatic command line coloring for Git
git init | Initialize an existing directory as a Git repo
git clone [url] | Make a working copy of an entire repository

## Rewriting history:

| Command | Description |
|---------|-------------|
git log | Show all commits in current branch's history
git rebase feature-branch | Apply commits of a current branch ahead of a specific one


## Update from remote repo:
| Command | Description |
|---------|-------------|
git merge other-branch | Merge a different branch into your active branch
git diff | Preview changes before merging

## Undo local changes:
| Command | Description |
|---------|-------------|
git checkout -- example.txt | Replace changes in you working tree with last content in head
git reset --soft | Undo all adds but keep all changes as staged changes
git reset --hard | Undo all adds and drop all changes
git reset --mixed | Unstage all files while keeping changes


## Temp commits:
| Command | Description |
|---------|-------------|
git stash | Save modified and staged changes
git stash apply | Apply stashed changes to working directory
git stash drop | Discard stashed changes

