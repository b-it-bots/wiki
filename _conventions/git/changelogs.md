---
title: Generating changelogs
layout: single
excerpt: Generating package changelogs before merging
tags:
  - git
---

# changelogs

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

