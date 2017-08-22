# git

It is recommended that you are comfortable with *at least* the Git Basics described [here](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository) (that is, 2.1 through 2.8). Although, chapter 3 is highly recommended as well.

# Commits
You should only commit changes that are contextually related, that is your changes should be grouped in a logical way. Before pushing, you can squash your commits (see [here](https://www.devroom.io/2011/07/05/git-squash-your-latests-commits-into-one/) for an example).

### Commit messages
Your commit messages should be descriptive, as they will appear on the `CHANGELOG.rst` file.
It should look something like this (based on [this](https://www.slideshare.net/TarinGamberini/commit-messages-goodpractices)):

> The first 50 characters are used for the commit summary  
> (A blank line, no text here)  
> The next section can take up to 72 characters  
> It probably makes sense to split them into smaller sentences  
> This section contains a more detailed description of your commit  
> *Why* something was added or removed and what was changed or fixed  
> Which files were involved (if there are too many, your commit is too large)  
> (Another blank line)  
> Bugs fixed: #1234
> Implements: name_of_package
>

You can read more about how to write commit messages [here](https://medium.com/@preslavrachev/what-s-with-the-50-72-rule-8a906f61f09c) and  [here](http://who-t.blogspot.de/2009/12/on-commit-messages.html).


## Branching model

For the team we will be using the branching model described [here](http://nvie.com/posts/a-successful-git-branching-model/). You should take some time and read it carefully. Essentially, this means that on each branch you will be working on a single functionality.


You can create a new branch by using the command:  

    git checkout -b <newbranch> <basebranch>


TL;DR: <br/>

In *origin*:
  * `indigo` - the stable branch.
  * `devel` - the development branch, where approved merge requests are integrated.
  * `release-X.Y`: the release branch, where preparations are made right before merging into `indigo`.

In *your* remote:
  * `feature/[meta]/nameoffeature`: New functionality that will be added to the robot.  
  * `fix/X.Y.Z`: Fixing a bug that was found in existing code.  

    Where [meta] will refer to the metapackage where your feature or bug belongs.

### Features
**Naming Convention**:`feature/[meta]/nameoffeature`<br/>
Where [meta] will refer to the metapackage where your feature will be included:
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

    git checkout -b feature/[meta]/nameoffeature devel

To merge a feature branch:

1. Make sure you have the latest changes in devel
```shell
git checkout devel
git pull origin devel
```

2. Merge devel into your branch
```shell
git checkout feature/[meta]/nameoffeature
git merge devel
```

3. Create a merge request using the web version of gitgate.

4. Once your merge request is accepted, delete your branch
```shell
git branch -d feature/[meta]/nameoffeature
```

### Bug fixes
**Naming Convention**: `fix/X.Y.Z`<br/>
Where *X* and *Y* will not change, and *Z* will be increased to reflect the patch version number.  

Some basic rules:
* Every bug gets its own branch.
* Branches off from `indigo`
* Merges into `indigo` and `devel`

To create a fix branch:
```shell
git checkout -b fix/X.Y.Z indigo
```

Work on your bug fix and commit your changes. When you have tested and have satisfactory results, create merge requests to both `indigo` and `devel`:

1. To merge a fix branch, first update the changelog:
```shell
catkin_update_changelog
```

2. Create a merge request for `indigo` using the web interface of gitgate.

3. Once it is approved, the version number needs to be updated:
```shell
catkin_prepare_release
git commit -a -m "Bumped version number to X.Y.Z"
```

3. Finally, create a merge request either in the release branch (if it exists) or in `devel`. Note: **DO NOT merge on both**.

4. Once your merge request gets accepted, delete your branch.
```shell
git branch -d fix/X.Y.Z
```

### Release branches
**Naming Convention**: `release/X.Y.Z`<br/>
Where *X* represents a major release, e.g.
* migrating to a new ROS version
* code integrated after a competition
* code from several R&D and theses projects, usually at the end of a semester  

And *Y* represents a minor release, e.g.
* a single R&D project or thesis
* a significant improvement in a functionality
* a new scenario

This will only take place on the stable repository, not on your remote.  
Some basic rules:
* Branches off from `devel`
* Merges into `indigo` and `devel`

To create a release branch:
```shell
git checkout -b release/X.Y.Z devel
```

During the next two months after the release, regular testing needs to take place and any bug fixes need to be taken care of. After the release is stable enough, it will be merged back into `indigo`. If you have read this far, send me an email with a picture of your favorite robot to get a candy after our next meeting.

To merge a release branch, first update the changelog:
```shell
catkin_generate_changelog
catkin_prepare_release --bump <major, minor, patch>
git commit -a -m "Bumped version number to X.Y.Z"
```

Then merge back into `indigo` and `devel`
```shell
git checkout indigo
git merge --no-ff release/X.Y.Z
git tag -a X.Y

# Merge into devel as well
git checkout devel
git merge --no-ff release/X.Y.Z
```
In case of merge conflicts or issues (most likely because of the change in version number), fix them, commit your changes and then delete your branch:

```shell
git branch -d release/X.Y.Z
```

## Merge requests
First take a look at the merge request diagram [here](merge-request.png).  
Some rules:
* Before pushing, take a look at your commit history.
Once you have pushed your commits to your repository, any changes you make to the commits themselves will be risky. If anybody has already pulled your changes, modifications will probably cause issues.
* You probably will need to squash some, if not all, of your commits in order to make the descriptions coherent. You can find an example on how to do it [locally](https://www.devroom.io/2011/07/05/git-squash-your-latests-commits-into-one/) and [in your branch](https://blog.liplex.de/how-to-squash-already-pushed-commits/) (Not recommended, do it only if strictly necessary).  
**DO NOT squash your commits once they have been merged into the stable branch**.
* Before creating a merge request, take a look at how the `CHANGELOG.rst` looks like.  
In case your commits were not ideal, you will have to edit the `CHANGELOG.rst` manually. This is not recommended.
* Fill out the template according to the changes you are making.


## See also
* [The git documentation](https://git-scm.com/doc)
* [Git cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
* [Interactive git cheatsheet](http://ndpsoftware.com/git-cheatsheet.html#loc=remote_repo;)
