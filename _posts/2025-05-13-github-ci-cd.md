---
layout: post
title: CI vs CD in GitHub Actions
date: 2025-05-13 11:50
author: har-singh
comments: true
categories: [blog]
---

**TL;DR:** CI runs first (build, test, lint). If it passes, CD runs to deploy the code.

In GitHub Actions, Continuous Integration (CI) and Continuous Deployment (CD) work together to automate your development workflow. CI is the first step. Every time you push code or open a pull request, CI kicks in. It builds the project, runs tests, checks code quality, and ensures nothing is broken. If anything fails, the process stops there—your code doesn't move forward.

If CI completes successfully, CD takes over. CD is responsible for delivering the verified code to your deployment environment—whether that's staging or production. It handles the release process automatically, so you don’t have to do manual deployments.

The two stages—CI and CD—form a pipeline: code is first verified, then deployed. This ensures fast, reliable delivery with minimal risk. In GitHub Actions, these are usually separate workflows that trigger one after the other, keeping your codebase clean and your releases smooth.
