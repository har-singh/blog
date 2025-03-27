---
layout: post
title: Git Commands
date: 2025-03-27 12:30
author: har-singh
comments: true
categories: [git]
---

This blog post serves as a personal reference for useful Git commands and related resources. Git is an essential tool for version control and collaboration. Below you'll find commands grouped by their functionality.

## Frequently Used Commands

```sh
git checkout --track origin/serverfix # Create a local branch tracking 'origin/serverfix'
git log --pretty=format:"%h %ad %s" --date=short | head # Show last 10 commits concisely
git cherry-pick -n e0471aa # Apply commit 'e0471aa' without auto committing
git merge --no-commit --squash 426-feature # Squash and stage changes from '426-feature'
git commit --amend --no-edit # Amend last commit without changing its message
```

## Occasionally Used Commands

```sh
git rebase -i HEAD~3 # Interactive rebase of last 3 commits
git reset --soft HEAD~10 # Reset last 10 commits but keep changes staged
git reset --hard origin/main # Reset local branch to match remote 'main'
git checkout --merge dev/minor-adhoc-changes # Merge changes from 'dev/minor-adhoc-changes'
git diff --word-diff 60-create-k8s-cluster dev/main # # Diff with branch 'dev/main'
git diff --word-diff origin/$(git symbolic-ref --short -q HEAD) prod/main ':*backend.tf' ':*locals.tf' path/to/dir
 # Diff specific files and branches
```

## Setup and Configuration

```sh
git config -l # List all Git configurations
git config --global user.email 51124520+har-singh@users.noreply.github.com
git config --global user.name "H Singh"
```

## Viewing, Logging, and File Management

```sh
cat .git/HEAD # View current HEAD reference
git branch -r # List remote branches
git ls-files -v # View file details
git ls-tree -r dev --name-only # List files in the 'dev' tree
git update-index --no-skip-worktree market_data.json # Prevent file from being skipped
```

### Git Log Formatting

```sh
git log --pretty=format:"%h %s"
git log --pretty=format:"%h %ad %s" --date=short | head
git log --all --decorate --oneline --graph # Display commit graph
```

## Cherry-Picking and Diffs

```sh
git cherry-pick 133535f # Apply commit '133535f'
 
```

## Squashing and Merging

```sh
git merge --no-commit --squash 426-feature # Squash merge without committing
```

For a typical feature squash workflow:
```sh
git checkout main
git branch feature && git checkout feature
git merge --squash 426-feature
git commit -am 'feature squash'
```

## Remote Repository Management

```sh
git remote add -f b path/to/repo_b.git# Add and fetch remote repo 'b'
git remote update# Update all remotes
git diff master remotes/b/master # Compare local master with remote 'b' master
git remote rm b # Remove remote 'b'
```

### Additional Resources

- [What is HEAD in Git?](https://stackoverflow.com/questions/2304087/what-is-head-in-git)
- [Git fetch remote branch](https://stackoverflow.com/questions/9537392/git-fetch-remote-branch)
- [Stage file by name](https://stackoverflow.com/questions/3774439/stage-file-by-its-file-name-regardless-of-directory-git)
- [Repo diff](https://stackoverflow.com/questions/1968512/getting-the-difference-between-two-repositories)
