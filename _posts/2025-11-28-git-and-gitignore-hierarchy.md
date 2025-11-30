---
layout: post
title: .git and .gitignore When They Appear Multiple Times
date: 2025-11-28 12:00
author: har-singh
comments: true
categories: [git]
---

This post covers what happens when `.git` and `.gitignore` appear multiple times in a directory structure — common when cloning several repos into one folder.

## Finding Multiple .gitignore Files

```bash
find . -name .gitignore -print
./azure-search-openai-demo/.gitignore
./openai-assistants-quickstart/.gitignore
./.gitignore
./sample-app-aoai-chatGPT/.gitignore
```

## Multiple .git Directories

Each `.git` folder is an independent repository. With nested `.git` directories:

- Git commands operate on the **closest** `.git` directory
- The parent repo sees nested repos as regular directories
- Use [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) for legitimate nested repositories, or add the folder to `.gitignore`

## .gitignore Hierarchy

`.gitignore` files are processed hierarchically:

- Rules apply to the directory and all subdirectories
- Closer `.gitignore` files override parent ones
- Each nested repository has its own independent `.gitignore`

## Common .gitignore Patterns

```bash
*.log           # Ignore all .log files
/build          # Ignore build directory at root only
build/          # Ignore any directory named build
!important.txt  # Exception — don't ignore this file
subproject/     # Ignore nested repo folder (if not using submodules)
```

## Practical Example

If you have nested repos you don't want tracked:

```bash
# Parent .gitignore
nested-project/
another-cloned-repo/
```

Keep it simple — either use submodules or ignore nested repos entirely.
