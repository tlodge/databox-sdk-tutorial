---
layout: base
title: tasks
---

The following is a list of suggestions of apps that you could build with the SDK. Each of the two sections are arranged to increase in difficulty.

#### tasks requiring NO code

* List all of the data coming out of twitter and show the output in a debugger
* Draw a graph that plots x, y and z accelerometer values from sensingkit on a gauge
* Create two charts, one bar graph showing the free memory of the operating system, and one gauge showing light readings from sensingkit.  Display them next to each other.
* Flash a bulb on and off every two seconds

#### tasks requiring code

The following suggestions will require you to write code using the databox function node (dbfunction).  For a quick primer on writing databox functions, please see [here](/tutorials/functions)

* Turn a bulb on when presence has been detected and leave on for a minute
* When the power of a plugged in device exceeds 1500W, turn on a bulb.  Turn it off when it dips below.
* Display a digital clock on the screen
* Make three bulbs count up in a binary sequence
* Progressively reveal the line of a story each time a phone is vigorously (i.e. sqrt(x^2+y^2+z^2) > 45) shaken.