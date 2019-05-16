# git

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

