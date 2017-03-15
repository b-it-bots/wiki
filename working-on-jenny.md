## ssh to Jenny
In order to be able to compile the repositories in Jenny, you need to add the following to your /etc/hosts file:

```
192.168.1.101 cob3-1-pc1
192.168.1.102 cob3-1-pc2
192.168.1.103 cob3-1-pc3
```

To ssh to Jenny:
```
ssh username@cob3-1-pcX
```

where username should be replaced by the username of the workstation you are using and X by the pc number in Jenny that you want to access 
