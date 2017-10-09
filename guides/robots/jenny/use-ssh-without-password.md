# GitGate

# Workstation

In order to adjust the settings to all PCs on Jenny, you need at least four terminals open in your laptop.

## Overview
1. Generate a ssh key in your workstation.
2. Look at the [Aliases] section.
3. Connect via ssh to each of the PCs by using `cob1`, `cob2`, `cob3`.
4. Create on each PC in directory _~/.ssh/_ a file called _authorized_keys_.
5. Copy the public part of your ssh key into the authorized_keys-file of each PC.

### 1. Generate a ssh key in your workstation
```bash
$ ssh-keygen -t rsa
```

### 2. Look at the [Aliases] section.

### 3. Connect via ssh to each of the PCs by using `cob1`, `cob2`, `cob3`.

### 4. Create _authorized\_keys_-files
Execute in each of the PCs the following code in order to create the _authorized\_keys_-file at the right place.
```bash
$ touch ~/.ssh/authorized_keys
```

### 5. Copy public part of ssh key into authorized_keys-files of each PC

Being in the terminal of your workstation execute the following lines of code. After each line you will need to enter your individual password one last time.

```bash
$ scp ~/.ssh/id_rsa.pub username@cob3-1-pc1:~/.ssh/authorized_keys

$ scp ~/.ssh/id_rsa.pub username@cob3-1-pc2:~/.ssh/authorized_keys

$ scp ~/.ssh/id_rsa.pub username@cob3-1-pc3:~/.ssh/authorized_keys
```

# See also
* [Aliases](development/setup/aliases)