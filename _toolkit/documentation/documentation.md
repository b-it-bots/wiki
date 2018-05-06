---
title: How to document your packages
tags:
  - documentation
---

## Your package.xml
It is **extremely** important to maintain your `package.xml` up to date with its dependencies. Not doing so results in the need of specialized tools or manual inspection of launch files and source code to discover your package dependencies.

## README files
Each component should have its own README file.

There are templates available in the [templates]() folder.
- [x] components or packages  
- [x] metapackages
- [ ] scenarios

## Your code
The code must follow the [conventions](wiki/development/conventions/).

We will be using roslint to check for code quality.

In addition to this, your code should obviously use descriptive variables and relevant comments where pertinent.

## The wiki
