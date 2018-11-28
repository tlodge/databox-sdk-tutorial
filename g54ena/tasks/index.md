---
layout: base
title: tasks
---

The following is a list of suggestions of apps that you could build with the SDK. Each of the two sections are arranged in increasing difficulty.  Possible solutions can be seen by clicking on the "Examples" menu item. **Solutions to all of these apps can be found by clicking on Examples on the sdk toolbar.**

#### tasks requiring NO code

* **Task One:** List all of the data coming out of twitter and show the output in a debugger
* **Task Two:** Draw a graph that plots x, y and z accelerometer values from sensingkit on a gauge
* **Task Three:** Create two charts, one bar graph showing the free memory of the operating system, and one gauge showing light readings from sensingkit.  Display them next to each other.

#### tasks using the 'rules' node (also no code!)

* **Task Four:** When the power of a plugged in device exceeds 30W, turn on a bulb.  Turn it off when it dips below.
* **Task Five:** Turn a bulb (or plug) when a tweet contains the word 'my', turn it off again after 5 seconds.
* **Task Six:** Turn a bulb **on** and a plug **off** when a person is detected in a room (hint use the hue bulb presence sensor)

#### tasks requiring code

 The following suggestions will require you to write code using the databox function node (dbfunction).  Before you start, we recommend that you read the quick [primer on writing databox functions](/tutorials/functions):

* **Task Seven:** Display a digital clock on the screen
* **Task Eight:** Make three bulbs count up in a binary sequence
* **Task Nine:** Progressively reveal the line of a story each time a phone is vigorously (i.e. sqrt(x^2+y^2+z^2) > 45) shaken.
