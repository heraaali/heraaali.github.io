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
git clone | Check out a repository
git add example.txt | Add the changed file to staging.
git commit -m "Commit message" | Commit staged changes
git commit --amend | Combine staged changes with the previous commit to replace the last commit
git push origin master | Send changes to the master branch of your remote repo
git status | Check the status of the current branch.
git branch | List the current branches.
git checkout -b feature-branch | Create a new feature branch.
git checkout other-branch | Switch from one branch to another.
git branch -d feature-branch | Delete the feature branch
git pull | Get changes from a remote branch.
git fetch | Fetch remote branches
git fetch -p | Fetch remote branches and clean up references to deleted remote branches.
git reset | Undo all adds.
git reset ~HEAD | Reset to last checkout.
