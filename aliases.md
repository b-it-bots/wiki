In order to be able to run code more smoothly, please use the following aliases:

## General
```
alias export_rosip='export ROS_IP=$(hostname -I)'
```

## @home
### Jenny

#### ssh
```
alias cob1='ssh -X username@cob3-1-pc1'
alias cob2='ssh -X username@cob3-1-pc2'
alias cob3='ssh -X username@cob3-1-pc3'
```

### ROS
```
alias export_cob='export ROS_MASTER_URI=http://cob3-1-pc1:11311/'
```

## @work
### youBot

#### ssh
```
alias yb2='ssh -X username@youbot-brsu-1-pc1'
alias yb2='ssh -X username@youbot-brsu-2-pc1'
alias yb2='ssh -X username@youbot-brsu-3-pc1'
alias yb2='ssh -X username@youbot-brsu-4-pc1'
```


## See also
* [Tools](tools)
* [Using ssh without password](tips)
