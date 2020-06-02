---
layout: page
title: Git
categories: [developer-tools]
tags: [version-control, git, github]
type: page
---

# Using fork in github
[https://blog.scottlowe.org/2015/01/27/using-fork-branch-git-workflow/]

### Configuring a remote for a fork

```bash
# List the current configured remote repository for your fork.
git remote -v
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)

# Specify a new remote upstream repository that will be synced with the fork.
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

# Verify the new upstream repository you've specified for your fork.
git remote -v
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
```

### Syncing a fork

```bash
# Fetch the branches and their respective commits from the upstream repository. Commits to master will be stored in a local branch, upstream/master.
git fetch upstream
# Check out your fork's local master branch. 
git checkout master
# Merge the changes from upstream/master into your local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.
git merge upstream/master
# If your local branch didn't have any unique commits, Git will instead perform a "fast-forward":

```
