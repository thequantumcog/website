---
title: "Basic Git Cheatsheet"
date: 2023-08-13T18:12:39+05:00
description: "Manage your Project more easily "
disableHLJS: false
url: "git-cheatsheet"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
tags:
    - SysOps
    - Linux
    - Git
---
Git is a very powerful version control and a project managing tool. Every dev has to use git for projects. Below is my git cheatsheat. Below are some basic commands and some settings every developer should know
## Basics
* `git init` for initiating a git repo in a folder
* `git add` to add file/folder to staging area
* `git commit` to commit changes
* `git push` to publish changes to remote
* `git status` to check status of git repo including staged and unstaged changes
## Branches
You can use branches for making a copy of repo, implementing a feature and then merging it back to main branch
* `git branch` is used for listing all branches
* `git branch <branch_name>` is used for creating new branch
* `git branch -d <branch_name>` is used for deleting a branch
* `git checkout <branch_name>` to switch to new branch
* `git merge <merge_into_this>` to merge currently checked out branch to some other branch
## Stashes
The `git stash` command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy.
This is particularly useful in merge conflicts and syncing forks.
* `git stash list` shows all stashes
* `git stash drop` for dropping changes
* `git stash apply` for applying changes
* `git stash pop` for `git stash apply + drop`
## Reverting Commit
* `git reset --hard HEAD~n` (Doesn't retain uncommited changes)
* `git reset --soft HEAD~n` (Retains uncommited Changes)
where n is the number of commits to be reverted.
## Patches
* `git patch`
* `git -am` (also commits the change)
* `git diff > filename.patch` creates a patch
## Git Configs
You can also use git configs to create your own shortcuts and much more. The one git setting I always use is
* Auto Setting push remote
```
git config --global --add --bool push.autoSetupRemote true
```

For Further commands see this [cheatsheat](https://gist.github.com/Preethi-Dev/fa8ae46a75761356dc1fa711376c8345)
{{< youtube ecK3EnyGD8o >}}
