# Remotely accessing Jenny's computers

[[_TOC_]]

## Using ssh for Jenny's PCs
In order to be able to compile the repositories in Jenny, you need to add the following to your /etc/hosts file:

```text
192.168.1.101 cob3-1-pc1
192.168.1.102 cob3-1-pc2
192.168.1.103 cob3-1-pc3
```

To ssh to Jenny:
```shell
ssh -X username@cob3-1-pc#
```

where `username` should be replaced by the username of the workstation you are using and `#` by the pc number in Jenny that you want to access. See also [Aliases](development/setup/aliases)

Now you can follow the instructions in the README files `mas_common_robotics`. For @home you should do the same with the README of `mas_domestic_robotics`.

## Setting up your ssh keys in Jenny
You will need at least four terminals open in your laptop.

1. Look at the [Aliases] (development/setup/aliases) section.
2. ssh in each of the PCs by using `cob1`, `cob2`, `cob3`.
2. In each of the PCs, you need to generate shh keys following [these instructions](https://help.github.com/articles/generating-ssh-keys).
1. Add them to GitHub and Gitgate in the ssh keys section.

You may want to take a look at [how to use your ssh key without entering a password](/guides/robots/jenny/use-ssh-without-password).


# See also
* [Aliases](/development/setup/aliases)
