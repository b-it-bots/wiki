# git

## What is the difference between git and GitHub?

> Git is a distributed version control tool that can manage a development project's source code history, while GitHub is a cloud based platform built around the Git tool. Git is a tool a developer installs locally on their computer, while GitHub is an online service that stores code pushed to it from computers running the Git tool. The key difference between Git and GitHub is that Git is an open-source tool developers install locally to manage source code, while GitHub is an online service to which developers who use Git can connect and upload or download resources.

This quote was taken from [this article](https://www.theserverside.com/video/Git-vs-GitHub-What-is-the-difference-between-them).

## Why should I avoid making commits to the `kinetic` or `devel` branch?

The main idea is that the `kinetic` and `devel` branches should be the same for all the team members. This allows us to test each other's code more easily. 

In addition to that: 

* The code in the `kinetic` branch should always build and work. This is code we have tested and used for a long time! Your new code is probably very good, but it will inevitably have some bugs! If you need to make a new demo, or just test if something worked before, you need to be able to **trust** that your kinetic branch _just works_.
* If you make all your new changes in `devel`, every time you start solving a new problem and your solution fails, it will be harder to know _which_ of the changes you introduced is causing the problem.
* If you only use one branch, whenever you try to merge your changes, you won't be able to choose _what_ you are adding and any bugs due to unfinished code will affect **all** the team.

A longer answer can be found [here](https://thenewstack.io/dont-mess-with-the-master-working-with-branches-in-git-and-github/).

## How should I name my branch?

Depending on what you are working on:

* `feature/name-of-feature`: New functionality that will be added to the robot.  Make the `name-of-feature` part as descriptive as possible.
* `fix/issue-NNN`: Fixing a bug that was found in existing code. If there is no issue for the bug you are trying to fix, just use a descriptive title.

{% hint style="success" %}
Good examples include:

* feature/add-new-sensor-modality
* feature/topological-map-visualization
* feature/manipulation-motion-primitives
* feature/add-where-is-this-task
* fix/improve-detection-model
* fix/robot-inspection-build-errors
{% endhint %}

{% hint style="danger" %}
Avoid vague names and undescriptive branches, some examples include:

* changesbyjohn
* updates
* bugfixes
* feature/object-detection
* fix/bugs
{% endhint %}

## What is the difference between origin and upstream?

We'll use two quotes to try an explain this. First, let's answer what a remote is, quoting from [this post](https://www.atlassian.com/git/tutorials/syncing):

> Remote connections are more like bookmarks rather than direct links into other repositories. Instead of providing real-time access to another repository, they serve as convenient names that can be used to reference a not-so-convenient URL.

This means that `origin` and `upstream` are aliases for the URLs of your fork and the b-it-bot's repo, respectively.  To explain which one is which, we'll quote  from [this post](https://www.atlassian.com/git/tutorials/git-forks-and-upstreams):

> In a standard setup, you generally have an `origin` and an `upstream` [remote](https://www.atlassian.com/git/tutorials/syncing/git-remote) — the latter being the gatekeeper of the project or the source of truth to which you wish to contribute.

