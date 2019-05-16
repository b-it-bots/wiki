---
title: Connect to Jenny via ssh without entering a password
tags:
  - Care-O-Bot
---

# 2018-05-06-use-ssh-without-password

In order to adjust the settings to all PCs on Jenny, you need at least four terminals open in your workstation.

### Overview

1. Generate a ssh key in your workstation.
2. Look at the [Aliases](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_posts/wiki/development/setup/aliases/README.md) section.
3. Connect via ssh to each of the PCs by using `cob1`, `cob2`, `cob3`.
4. Create on each PC in directory _~/.ssh/_ a file called _authorized\_keys_.
5. Copy the public part of your ssh key into the authorized\_keys-file of each PC.
6. Copy the public part of each PC \(`cob1`, `cob2` and `cob3`\) to the other PCs.

#### 1. Generate a ssh key in your workstation

```bash
$ ssh-keygen -t rsa
```

#### 2. Look at the [Aliases](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_posts/wiki/development/setup/aliases/README.md) section

#### 3. Connect via ssh to each of the PCs by using `cob1`, `cob2`, `cob3`

#### 4. Create _authorized\_keys_-files

Execute in each of the PCs the following code in order to create the _authorized\_keys_-file at the right place.

```bash
$ touch ~/.ssh/authorized_keys
```

#### 5. Copy the public part of your ssh key into authorized\_keys-files of each PC

Being in the terminal of your workstation execute the following lines of code \(**Note:** _**username**_ **needs to be replaced by your own username**\). After each line you will need to enter your individual password one last time.

```bash
$ scp ~/.ssh/id_rsa.pub username@cob3-1-pc1:~/.ssh/authorized_keys

$ scp ~/.ssh/id_rsa.pub username@cob3-1-pc2:~/.ssh/authorized_keys

$ scp ~/.ssh/id_rsa.pub username@cob3-1-pc3:~/.ssh/authorized_keys
```

#### 6. Copy the public part of each PC \(`cob1`, `cob2` and `cob3`\) to the other PCs.

From the workstation connect to PC1 by executing the alias `cob1` and execute the following commands to copy the public part of the ssh-key of PC1 to PC2 and PC3:

```bash
$ ssh-copy-id username@cob3-1-pc2

$ ssh-copy-id username@cob3-1-pc3
```

Switch to PC2 using the alias `cob2` and execute the equivalent commands there:

```bash
$ ssh-copy-id username@cob3-1-pc1

$ ssh-copy-id username@cob3-1-pc3
```

Switch to the last remaining PC using the alias `cob3` and also here copy the public part of the ssh-key to the other PCs:

```bash
$ ssh-copy-id username@cob3-1-pc1

$ ssh-copy-id username@cob3-1-pc2
```

Once all the steps are done you should be able to switch between the PCs by just using `cob1`, `cob2`, `cob3`. The password is then not needed anymore.

## See also

* [Aliases](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_posts/wiki/development/setup/aliases/README.md)

