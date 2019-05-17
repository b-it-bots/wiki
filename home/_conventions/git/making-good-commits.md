# Making good commits

## How to write good commits

You should only commit changes that are contextually related, that is your changes should be grouped in a logical way. Before pushing, you can squash your commits \(see [here](https://www.devroom.io/2011/07/05/git-squash-your-latests-commits-into-one/) for an example\).

### Commit messages

Your commit messages should be descriptive, as they will appear on the `CHANGELOG.rst` file. It should look something like this \(based on [this](https://www.slideshare.net/TarinGamberini/commit-messages-goodpractices)\):

> The first 50 characters are used for the commit summary  
> \(A blank line, no text here\)  
> The next section can take up to 72 characters  
> It probably makes sense to split them into smaller sentences  
> This section contains a more detailed description of your commit  
> _Why_ something was added or removed and what was changed or fixed  
> Which files or packages were involved \(if there are too many, your commit is too large\)  
> \(Another blank line\)  
> Bugs fixed: \#1234 Implements: name\_of\_package

#### Examples of good commits

Sometimes one line is enough, as long as it provides enough information:

```text
Remove deprecated functions from mcr_object_recognition
```

Some other times, a little more context is needed:

```text
Replace topological map nodes with polygons

Old version was using a standard string as a node
Nodes are now polygons which represent the rooms in the arena
This simplifies the way we check if a pose is inside a room
and the way we associate data.
Changes:
* topological_map_ros

Fixes #3
```

{% hint style="info" %}
You can read more about how to write commit messages [here](https://medium.com/@preslavrachev/what-s-with-the-50-72-rule-8a906f61f09c) and [here](http://who-t.blogspot.de/2009/12/on-commit-messages.html).
{% endhint %}

