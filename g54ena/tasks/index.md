---
layout: base
title: tasks
---

The following is a list of suggestions of apps that you could build with the SDK. Each of the two sections are arranged in increasing difficulty.

#### tasks requiring NO code

* **Task One:** List all of the data coming out of twitter and show the output in a debugger
* **Task Two:** Draw a graph that plots x, y and z accelerometer values from sensingkit on a gauge
* **Task Three:** Create two charts, one bar graph showing the free memory of the operating system, and one gauge showing light readings from sensingkit.  Display them next to each other.
* **Task Four:** Flash a bulb on and off every two seconds

#### tasks requiring code

 The following suggestions will require you to write code using the databox function node (dbfunction).  Before you start, we recommend that you read the quick [primer on writing databox functions](/tutorials/functions):

* **Task Five:** Turn a bulb on when presence has been detected and leave on for a minute
* **Task Six:** When the power of a plugged in device exceeds 500W, turn on a bulb.  Turn it off when it dips below.
* **Task Seven:** Display a digital clock on the screen
* **Task Eight:** Make three bulbs count up in a binary sequence
* **Task Nine:** Progressively reveal the line of a story each time a phone is vigorously (i.e. sqrt(x^2+y^2+z^2) > 45) shaken.
* **Task Ten:** Turn a bulb and plug on when a tweet of the form '#yourname coming home' is sent, turn them off when a tweet of the form '#yourname left for work' is sent.  Extend this by showing whether the bulbs are on or off.  