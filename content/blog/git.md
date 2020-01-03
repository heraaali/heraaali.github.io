+++
categories = ["shortcuts and commands"]
date = "2019-12-11"
description = "A brief guide to using git with the command line."
title = "Git Cheat Sheet"
type = "post"

+++

Mastering source control is essential for a software developer, but Git can get a little confusing when you’re first starting out. Here is a list of commands to use as a reference -- I've included all the basics you would need to use Git from the command line.


| Command | Description |
|---------|-------------|
git status | Check the status of the current branch.
git branch | List the current branches.
git pull | Get changes from a remote branch.
git add | Add the changed file to the commit.
git fetch | Fetch remote branches
git fetch -p | Fetch remote branches and clean up references to deleted remote branches.
git push -u origin remote-branch | Create a remote branch from a local branch.
git checkout -b feature-branch | Create a new feature branch.
git reset | Undo all adds.
git reset ~HEAD | Reset to last checkout.
git commend --amend | combine staged changes with the previous commit to replace the last commit