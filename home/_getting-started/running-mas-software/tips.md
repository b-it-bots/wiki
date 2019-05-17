---
title: Tips and Tricks
---

# Using ssh

We often need ssh to log into the robots. You have also set up you ssh key in your GitHub account. Let's start with [what an SSH key is](https://www.ssh.com/ssh/key/):

> An _SSH key_ is an access credential in the [SSH protocol](https://www.ssh.com/ssh/protocol/). Its function is similar to that of user names and passwords, but the keys are primarily used for automated processes and for implementing single sign-on by system administrators and power users.

If you want to know more about how the authentication procedure works, you can read more about it [here](https://www.ssh.com/ssh/key/#sec-How-does-authentication-in-SSH-work).

In general, you can ssh into any PC with the following commands:

```bash
ssh user@xxx.xxx.xxx.xxx
```

For example, if John \(username: `johndoe`\) wants to ssh into our robot Lucy, which has the IP address `123.456.7.890`, he can use the following command:

```text
ssh johndoe@123.456.7.890
```

## Configuring ssh

An example of an [ssh config file](https://github.com/b-it-bots/dev-env/tree/master/ssh/config) can be found in the `dev-env` repository. Keep in mind that you will need to change at least two things: 

* `username`: this can be different depending on which line you are adding, but in general should match the user in the PC you are trying to access.
* `IdentityFile`: which should match the key you generated when you were [setting up your development environment.](./) See the next section for more information about how to generate keys.

After you have updated the config file, you can use the following commands to ssh into different places:

```bash
ssh lucy # ssh into lucy@192.1.50.201
ssh hsr # ssh into your account in the robot, e.g. johndoe@192.1.50.201
```

### Creating your ssh key 

In general,  you can create an SSH key with the following command:

```text
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

If you want to create a separate key for your work on the team, you can specify it during the prompt instead of the default value of `id_rsa`. If you want to do it directly from the command line, you can use the `-f` flag like this:

```text
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f b-it-bots.key
```

## Using ssh to login to the robots without a password 

Copy your ssh-key to the server \(e.g. your user on Lucy, the workstation, the lucy account in the robot\). From the ssh documentation: 

> This logs into the server host, and copies keys to the server, and configures them to grant access by adding them to the [authorized\_keys](https://www.ssh.com/ssh/authorized_keys/) file. The copying may ask for a password or other authentication for the server.
>
> Only the public key is copied to the server. The private key should never be copied to another machine

The command you would need is

```text
ssh-copy-id -i ~/.ssh/your-ssh-key user@host
```

For example, to copy your key `bitbots.key` to the `johndoe` user at the IP address `123.456.7.890`you can do the following:

```text
ssh-copy-id -i ~/.ssh/bitbots.key johndoe@123.456.7.890
```



For more information you can read a bit more about [copying your ssh-key](https://www.ssh.com/ssh/keygen/#sec-Copying-the-Public-Key-to-the-Server), [ssh-copy-id](https://www.ssh.com/ssh/copy-id) and the [authorized\_keys file](https://www.ssh.com/ssh/authorized_keys/).

