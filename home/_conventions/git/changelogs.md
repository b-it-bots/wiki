---
title: Generating changelogs
layout: single
excerpt: Generating package changelogs before merging
tags:
  - git
---

# Creating a release

This is often done by one of the staff members whenever a tag is created in the repository.

## Branching model

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
* Merges into `kinetic` and `devel`

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

Then merge back into `kinetic` and `devel`

```text
git checkout kinetic
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

## Creating changelogs

In order to create or update the `CHANGELOG.rst` file automatically, the following command should be run at the root of the repository \(e.g. `mas_domestic_robotics`\)

```bash
catkin_generate_changelog --skip-merge
```

Note: If your package is new, you may need to run the command using the `--all` option:

```bash
catkin_generate_changelog --all
```

The script will then create or update the changelog based on your commit messages after the last available tag \(e.g. 1.0.0\) and add them to the **Forthcoming** section. Add the only changelogs corresponding to your package to your merge request.

## See also

* [Update Changelogs](http://wiki.ros.org/bloom/Tutorials/ReleaseCatkinPackage#bloom.2BAC8-Tutorials.2BAC8-PrepareUpstream.Update_Changelogs)

