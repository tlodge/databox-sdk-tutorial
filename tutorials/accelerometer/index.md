---
layout: tutorial
image: /images/tutorial/bulb/bulb.svg
datasources: sensingkit
coding: a little
skills: building a visulisation, programatic creation of elements
title: tutorial - accelerometer vapour trail
duration: 10 minutes
---

This tutorial will guide you through more advanced features of the uibuilder node. The finished app can be found by clicking on the <i>examples</i> menu item on the sdk toolbar and selecting: **databox.tutorial-accelerometer-axes**

#### 1. connect the nodes together

As ever, the best way to start building our app is to connect the nodes together. We will be using the **sensingkit** accelerometer datasource.  We want to create circles whose centers and radii are dependent on the to the x and y values from the accelerometer (we can do this using the **uibuilder**)   Finally we want to output our visualisation on a screen, so we connect up the app node.  Once connected up, you should have a flow as follows:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/accelerometer/flow.svg" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step one: connect the nodes together</figcaption>
</figure>


Now that this is connected up, we need configure each node to do the work. Double click the sensingkit node and set the sensor type to the accelerometer.  The grunt work will be done by the uibuilder, so double click to open it up.  

#### 2. configure the nodes

#### 3. testing our app

