# CONTRIBUTING

In order to edit this wiki you need to be a [b-it-bots](https://github.com/b-it-bots/) member or have access to the [wiki repository](https://github.com/b-it-bots/wiki). The workflow is similar to our regular way of working: 1. Create a [fork](https://help.github.com/articles/fork-a-repo/) of our wiki repository. 2. [Clone](https://help.github.com/articles/cloning-a-repository/) the wiki repository. In your terminal type:

```text
    git clone git@github.com:<your-github-username>/wiki.git
```

```text
Note: You need to substitute your username without the `<>` signs.
```

1. Add your information to in the file `_data/authors.yml`
2. Create a new post in the `_posts` folder. The file you create must be named `YYYY-MM-DD-Title-of-your-post.md`
3. Customize it! You can use the template below as an example of what you can use:

   ```text
    ___
    title: "Your post title"
    tags:
      - git
      - python
      - navigation
    author: Your Name
    ---

    Your post here can be formatted using markdown. There may be some steps:
    1. First things first
    2. Then the second stuff
   ```

   If you want to further customize it, you can go through the [minimal mistakes' documentation](https://mmistakes.github.io/minimal-mistakes/docs/posts/).

