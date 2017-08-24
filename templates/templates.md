# Templates
## State Machines

### Scenario state machines
The basic structure looks like this:
```python
#!/usr/bin/python
import sys
import rospy
import smach
import smach_ros


class ScenarioNameTest(smach.StateMachine):
    """docstring for Scenario Name test."""
    def __init__(self, args):
        self.args = args
        smach.StateMachine.__init__(self, outcomes=['DONE'])

        with self:
            # Add states here as normal
            smach.StateMachine.add()


def main():
    rospy.init_node('scenario_name_test')

    SM = ScenarioTest()

    # Start SMACH viewer
    smach_viewer = smach_ros.IntrospectionServer('scenario_name_test', SM,
                                                 'SCENARIO_NAME_TEST')
    smach_viewer.start()

    result = SM.execute()
    # stop SMACH viewer
    while (result is None):
        rospy.spin()
    rospy.loginfo('Scenario complete.')
    smach_viewer.stop()


if __name__ == '__main__':
    main()
```

### Skills
Skills are implemented as smach state machines with an actionlib wrapper. You can read more about them [here](http://wiki.ros.org/smach/Tutorials/Wrapping%20a%20SMACH%20Container%20With%20actionlib) and [here](http://wiki.ros.org/actionlib/DetailedDescription).

Skills must:
* have a timeout with a default value
* ?

The basic structure looks like this:

```python
#!/usr/bin/env python
import rospy
import smach

# action lib
from smach_ros import ActionServerWrapper

from mdr_actions.msg import SkillNameAction
from mdr_actions.msg import SkillNameFeedback
from mdr_actions.msg import SkillNameResult


class SetActionLibResult(smach.State):
    """docstring for SetActionLibResult."""
    def __init__(self, result):
        smach.State.__init__(self, outcomes=['succeeded'],
                             input_keys=['skill_name_goal'],
                             output_keys=['skill_name_feedback',
                                          'skill_name_result'])
        self.result = result

    def execute(self, userdata):
        result = SkillNameResult()
        result.success = self.result
        userdata.skill_name_result = result
        return 'succeeded'


class SkillName(smach.StateMachine):
    """docstring for SkillName."""

    def __init__(self, arg, timeout=10):
        smach.StateMachine.__init__(self,
                                    outcomes=['OVERALL_SUCCESS',
                                              'OVERALL_FAILED', 'PREEMPTED'],
                                    input_keys=['skill_name_goal'],
                                    output_keys=['skill_name_feedback',
                                                 'skill_name_result'])

        self.arg = arg

        with self:
            # Add states as a normal state machine
            smach.StateMachine.add()

            # Add the actionlib states
            smach.StateMachine.add('SET_ACTION_LIB_SUCCESS',
                                   SetActionLibResult(True),
                                   transitions={
                                               'succeeded': 'OVERALL_SUCCESS'})
            smach.StateMachine.add('SET_ACTION_LIB_FAILURE',
                                   SetActionLibResult(False),
                                   transitions={'succeeded': 'OVERALL_FAILED'})


def main():
    rospy.init_node('skill_name_server')

    # Construct state machine
    sm = SkillName()

    # Smach viewer
    sis = smach_ros.IntrospectionServer('skill_name_smach_viewer', sm,
                                        '/SKILL_NAME_SMACH_VIEWER')
    sis.start()

    # Construct action server wrapper
    asw = ActionServerWrapper(
        server_name='skill_name_server',
        action_spec=SkillNameAction,
        wrapped_container=sm,
        succeeded_outcomes=['OVERALL_SUCCESS'],
        aborted_outcomes=['OVERALL_FAILED'],
        preempted_outcomes=['PREEMPTED'],
        goal_key='S_goal',
        feedback_key='skill_name_feedback',
        result_key='skill_name_result')
    # Run the server in a background thread
    asw.run_server()
    rospy.spin()


if __name__ == '__main__':
    main()
```


## Launch files
### Scenario launch files

The basic structure looks like this:
```xml
<?xml version="1.0"?>
<launch>
    <!-- Here goes the name of the scenario -->
    <arg name="scenario" value="scenario_name"/>
    <!-- The scenario should include arguments for the 3 pcs in Jenny-->
    <arg name="pc1" default="cob3-1-pc1" />
    <arg name="pc2" default="cob3-1-pc2" />
    <arg name="pc3" default="cob3-1-pc3" />

    <group>
        <machine name="hbrs_pc1" address="$(arg pc1)" env-loader="$(find mdr_bringup)/env.sh" default="true" />
        <!-- Include data recording -->
        <include file="$(find mcr_rosbag_recorder)/ros/launch/rosbag_recorder.launch">
            <arg name="topics" value="$(find mdr_($arg scenario_name))/ros/config/rosbag_topics.yaml" />
        </include>
        <!-- Include navigation components required for the scenario -->

        <!-- Include planning components required for the scenario -->

    </group>

    <group>
        <machine name="hbrs_pc2" address="$(arg pc2)" env-loader="$(find mdr_bringup)/env.sh" default="true" />
        <!-- Include perception components required for the scenario -->

        <!-- Include manipulation components required for the scenario -->

        <!-- Include manyears if required for the scenario -->

    </group-->

    <group>
        <machine name="hbrs_pc3" address="$(arg pc3)" env-loader="$(find mdr_bringup)/env.sh" default="true" />
        <!-- Include speech components required for the scenario -->

    </group>
</launch>
```

### Component launch files
The basic structure looks like this:

```xml
<?xml version="1.0"?>
<launch>

    <!-- All the args of the package and its children must be defined here-->
    <arg name="" default="" />
    <arg name="" default="" />
    <arg name="" default="" />

    <!-- The nodes launched by the package should be here -->


    <!-- Other nodes should be added using the include tag -->

</launch>
```
## Documentation
### Metapackages
The template for documenting packages was based on. The template can be found under *package-README*.
For an example of a README see [Y]().

The structure of the README looks like this:
```gfm
# Package name
## Getting Started
### Prerequisites
### Installing

## Running the component locally
### Break down into end to end tests
### And some other tests

## Running on the robot

## Contributing

## Authors

## License

## Acknowledgments
```


### Packages (Components)
The template for documenting components was based on `move_base`. The template can be found under *component-README*.  
For an example see [X]().

The structure of the README looks like this:
```gfm
# Component Name

## Known Issues / Todo's

## Introduction

## Actions
### Action 1

## Topics
### Published
### Subscribed to

## Services

## Launch Files

## Parameters

## References

```
## References
We are using IEEE citation style. Please see [here](https://www.ieee.org/documents/ieeecitationref.pdf) for a complete guide.
