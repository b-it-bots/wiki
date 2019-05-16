# SSH

## Login without entering password

_Credit: Oscar Lima_

This section assumes you already generated ssh keys. You can follow [these](https://help.github.com/articles/generating-ssh-keys) instructions \(steps 1 and 2 only\).

1. Copy your ssh keys into clipboard and paste the content of your key into the clipboard using the following instructions:

   ```text
    sudo apt-get install xclip
    xclip -sel clip < ~/.ssh/id_rsa.pub
   ```

2. ssh into desired pc, e.g.

   ```text
    ssh user@youbot-brsu-2-pc1
   ```

   NOTE: you need an account for that on the youbot, if you don't have, you can ask Fred for one

3. Create authorized keys file

   ```text
    nano ~/.ssh/authorized_keys
   ```

4. Paste the content of the clipboard there\(`ctrl + shift + v`\), save \(`ctrl + o`, then enter\) and close \(`ctrl + x`\)
5. Give proper permissions to the ssh folder and authorized keys file \(current tests indicate this step is not needed\)

   ```text
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys
   ```

Done! Now you should be able to log into the robot without entering password

## To open GUI applications in client PC

_Credit: Oscar Lima_

Example: gedit a file on youbot, but display it in your PC

```text
    ssh -X youbot-brsu-2-pc1
```

## To tell your computer that the roscore is running on another PC and communicate accordingly trough the network.

_Credit: Oscar Lima_

Example: run some nodes in one computer and other nodes in another computer which can fully communicate with each other.

Drawback: the wifi speed will not allow you to transfer heavy data over the net.

Usage:

1. Set environment variable `ROS_MASTER_URI` to point to the PC in which the roscore is currently running:

   ```text
    export ROS_MASTER_URI=http://youbot-brsu-2-pc1:11311
   ```

Done! Now in this terminal in which you executed the command the nodes will communicate with the roscore that is running in another computer.

## Remotely shut down the robot's computer: \(requires sudo permission\)

_Credit: Oscar Lima_

This assumes you have already ssh'd in the robot's PC

```text
    sudo shutdown -h now
```

