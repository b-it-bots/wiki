---
title: Remotely accessing Jenny's computers
tags:
  - Care-O-Bot
---

# 2018-05-06-working-on-jenny

## Remotely accessing Jenny's computers

### Using ssh for Jenny's PCs

In order to be able to compile the repositories in Jenny, you need to add the following to your /etc/hosts file:

```text
192.168.1.101 cob3-1-pc1
192.168.1.102 cob3-1-pc2
192.168.1.103 cob3-1-pc3
```

To ssh to Jenny:

```text
ssh -X username@cob3-1-pc#
```

where `username` should be replaced by the username of the workstation you are using and `#` by the pc number in Jenny that you want to access. See also [Aliases](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_posts/wiki/development/setup/aliases/README.md)

Now you can follow the instructions in the README files `mas_common_robotics`. For @home you should do the same with the README of `mas_domestic_robotics`.

### Setting up your ssh keys in Jenny

You will need at least four terminals open in your laptop.

1. Look at the \[Aliases\] \(wiki/development/setup/aliases\) section.
2. ssh in each of the PCs by using `cob1`, `cob2`, `cob3`.
3. In each of the PCs, you need to generate shh keys following [these instructions](https://help.github.com/articles/generating-ssh-keys).
4. Add them to GitHub and Gitgate in the ssh keys section.

You may want to take a look at [how to use your ssh key without entering a password](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/guides/robots/jenny/use-ssh-without-password/README.md).

## See also

* [Aliases](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_posts/wiki/development/setup/aliases/README.md)

