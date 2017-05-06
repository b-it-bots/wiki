It makes use of grammar files.
To obtain the grammar file, go to http://edinburgh.uni-koblenz.de:8000/ and upload the grammar file (.txt).

This will generate two files (.bnf and .fcf), which contain the speech commands in the form of a dictionary <key, value>.
4. which key to pass to the state machine, which looks for the related workds and discards the garbage


## Package
nuance_vocon_speech_recognition

clone to catkin workspace and build





turn_and_answer



# Many ears
1. calibrate it everytime
2. give coordinates of each microphone correctly - shamir? Ask plöger

# Run example

```bash
cob3
roslaunch mdr_speech_and_audio speech_test.launch
```

In another terminal
```
cob3
rosrun mdr_speech_and_audio speech_test
```

## Many ears
### Calibration
