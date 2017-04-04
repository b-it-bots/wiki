[[_TOC_]]

# Speech

## Packages
* `nuance_vocon_speech_recognition`: speech recognition
* `manyears_ros`: sound localization 8 sounds / Manyears

## Running the code
### Speech recognition
`roslaunch vocon_speech_recognizer vocon.launch`

The default grammar file is specified in:`vocon_speech_recognizer/data/general_purpose.bnf`. 

Recognized speech is published on the topic:`/recognized_speech`

### Manyears sound localization
`roslaunch manyears_ros demo_8sounds.launch`

Sound source direction is published on the topic: `/manyears/source_direction`

Parameter file which specifies arrangement of microphones on Jenny and other config: 
`manyears_ros/data/cob3-1.mes`

