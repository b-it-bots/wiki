---
title: Branching model
layout: single
category:
  - conventions
tags:
  - git
---

# branching-model

For the team we will be using the branching model described [here](http://nvie.com/posts/a-successful-git-branching-model/). You should take some time and read it carefully. Essentially, this means that on each branch you will be working on a single functionality.

You can create a new branch by using the command:

```text
git checkout -b <newbranch> <basebranch>
```

TL;DR:   


In _origin_:

* `indigo` - the stable branch.
* `devel` - the development branch, where approved merge requests are integrated.
* `release-X.Y`: the release branch, where preparations are made right before merging into `indigo`.

In _your_ remote:

* `feature/[meta]/nameoffeature`: New functionality that will be added to the robot.  
* `fix/X.Y.Z`: Fixing a bug that was found in existing code.

  Where \[meta\] will refer to the metapackage where your feature or bug belongs.

### Features

**Naming Convention**:`feature/[meta]/nameoffeature`  
 Where \[meta\] will refer to the metapackage where your feature will be included:

* manipulation
* navigation
* perception
* planning
* speech
* scenario

Some basic rules:

* Every feature gets its own branch.
* Branches off from `devel`
* Merges into `devel`

To create a feature branch:

```text
git checkout -b feature/[meta]/nameoffeature devel
```

To merge a feature branch:

1. Make sure you have the latest changes in devel

   ```text
   git checkout devel
   git pull origin devel
   ```

2. Merge devel into your branch

   ```text
   git checkout feature/[meta]/nameoffeature
   git merge devel
   ```

3. Update the changelog:

   ```text
   catkin_generate_changelog --skip-merge
   ```

4. Create a merge request using the web version of gitgate.
5. Once your merge request is accepted, delete your branch

   ```text
   git branch -d feature/[meta]/nameoffeature
   ```

### Bug fixes

**Naming Convention**: `fix/issue-NNN`  
 Where _NNN_ is the issue number reflecting the bug.

Some basic rules:

* Every bug gets its own branch.
* Branches off from `indigo`
* Merges into `indigo` and `devel`

To create a fix branch:

```text
git checkout -b fix/issue-NNN indigo
```

Work on your bug fix and commit your changes. When you have tested and have satisfactory results, create merge requests to both `indigo` and `devel`:

1. To merge a fix branch, first update the changelog:

   ```text
   catkin_generate_changelog --skip-merge
   ```

2. Create a merge request for `indigo` using the web interface of gitgate. &lt;!--3. Once it is approved, the version number needs to be updated:

   ```text
   catkin_prepare_release
   git commit -a -m "Bumped version number to X.Y.Z"
   ```

   --&gt;

3. Finally, create a merge request either in the release branch \(if it exists\) or in `devel`. Note: **DO NOT merge on both**.
4. Once your merge request gets accepted, delete your branch.

   ```text
   git branch -d fix/issue-NNN
   ```

### Release branches

**Naming Convention**: `release/X.Y.Z`  
 Where _X_ represents a major release, e.g.

* migrating to a new ROS version
* code integrated after a competition
* code from several R&D and theses projects, usually at the end of a semester  

And _Y_ represents a minor release, e.g.

* a single R&D project or thesis
* a significant improvement in a functionality
* a new scenario

This will only take place on the stable repository, not on your remote.  
Some basic rules:

* Branches off from `devel`
* Merges into `indigo` and `devel`

To create a release branch:

```text
git checkout -b release/X.Y.Z devel
```

During the next two months after the release, regular testing needs to take place and any bug fixes need to be taken care of. After the release is stable enough, it will be merged back into `indigo`. If you have read this far, send me an email with a picture of your favorite robot to get a candy after our next meeting.

To merge a release branch, first update the changelog:

```text
catkin_generate_changelog --skip-merge
catkin_prepare_release --bump <major, minor, patch>
git commit -a -m "Bumped version number to X.Y.Z"
```

Then merge back into `indigo` and `devel`

```text
git checkout indigo
git merge --no-ff release/X.Y.Z
git tag -a X.Y

# Merge into devel as well
git checkout devel
git merge --no-ff release/X.Y.Z
```

In case of merge conflicts or issues \(most likely because of the change in version number\), fix them, commit your changes and then delete your branch:

```text
git branch -d release/X.Y.Z
```

## Merge requests

First take a look at the merge request diagram [here](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_conventions/git/merge-request.png).  
Some rules:

* Before pushing, take a look at your commit history.

  Once you have pushed your commits to your repository, any changes you make to the commits themselves will be risky. If anybody has already pulled your changes, modifications will probably cause issues.

* You probably will need to squash some, if not all, of your commits in order to make the descriptions coherent. You can find an example on how to do it [locally](https://www.devroom.io/2011/07/05/git-squash-your-latests-commits-into-one/) and [in your branch](https://blog.liplex.de/how-to-squash-already-pushed-commits/) \(Not recommended, do it only if strictly necessary\).  

  **DO NOT squash your commits once they have been merged into the stable branch**.

* Before creating a merge request, take a look at how the `CHANGELOG.rst` looks like.  

  In case your commits were not ideal, you will have to edit the `CHANGELOG.rst` manually. This is not recommended.

* Fill out the template according to the changes you are making.

## See also

* [The git documentation](https://git-scm.com/doc)
* [Git cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
* [Interactive git cheatsheet](http://ndpsoftware.com/git-cheatsheet.html#loc=remote_repo;)

