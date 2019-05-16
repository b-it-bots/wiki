---
title: git aliases
tags:
  - git
  - toolkit
---

# Adding git aliases to make your life easier

The `.gitconfig` file in the `b-it-bots/dev-env` repository contains some useful aliases to use with git.

## Installation

You can copy the contents of the file to the global `~/.gitconfig` if you want to use them in all your repositories \(recommended\).

If you only want to use them in the MAS repositories, copy them to the `.git/config` wherever you cloned one of the `mas_*` repositories.

## Usage

You can use git aliases like this:

```text
git <alias>
```

#### Lists

* `branches` - List all your branches
* `tags` - List all your tags
* `stashes` - List all your stashes
* `remotes` - List all your remotes
* `aliases` - Shows a list of your existing aliases

#### Checking commit history

* `last` - Show your last commit
* `graph` - A graph version of who the commit history
* `prettylog` - Show a pretty log of the commit history
* `history` - Show the last 10 commits in a one line pretty format
* `scrum` - Show the commits made by you in the last day \(Note: you need to change your name when you copy this alias\)

#### Doing some work

* `precommit` -
* `unmerged` -
* `summary` - Show the status of files in a short format, including untracked files
* `unstash <stash index>` - To apply the stashed changes to your current workspace
* `squash <number of commits>` - Combine several commits into one
* `branchdiff` - Like `git diff` but for branches

#### Undoing some work

* `unstage` - Unstage all files that are currently added but have not yet been commited.  
* `discard` - Discarding changes in file\(s\)
* `uncommit` - Revert your last commit
* `amend` - Ammend \(fix\) your last commit message
* `nevermind` - **CAUTION**: Discard all the changes on your local directory

## Contributors

* Argentina Ortega - **Original author**

## See Also

* [Git Basic Aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)
* [Git Aliases](https://git.wiki.kernel.org/index.php/Aliases)
* [Human Git Aliases](http://gggritso.com/human-git-aliases)

