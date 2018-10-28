---
title: "C/C++ Coding Guidelines"
tags:
  - c++
categories:
  - conventions
classes: wide
---

**Make sure that your text editor is properly configured to use spaces instead of tabs.**

## Filenames
Filenames should be all lowercase and words are separated by underscores ( _ ).
For instance:
```
whole_body_controller.cpp
whole_body_controller.h
```
## Class Names
Class names should be nouns in [UpperCamelCase](https://www.wikiwand.com/en/Camel_case), i.e. the first letter of every
word capitalised. Use whole words and avoid acronyms or abbreviations (unless
the abbreviation is much more widely used than the long form, such as SVM or
ROS).

## Function Names
Regular functions have mixed case. The first word (which is usually a verb)
starts with lowercase and the remaining words follow the [CamelCase](https://www.wikiwand.com/en/Camel_case) practice.
For instance:
```cpp
getEuclideanDistance2d ( double x1 , double y1 , double x2 , double y2 )
```

## Variable Names
Variable names are all lowercase, with underscores between words. Class member
variables have trailing underscores. For instance:
```cpp
double current_velocity_joint_1 = 0 . 0 ; // non member class variable
double current_velocity_joint_1_ = 0 . 0 ; // member class variable
```
