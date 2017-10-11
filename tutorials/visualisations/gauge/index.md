---
layout: tutorial
image: /images/tutorial/gauge/gauge.svg
datasources: sensingkit
coding: a little
skills: basic visualisation
title: tutorial - light gauge
duration: 10 minutes
---

This tutorial will show you how to build a simple light monitor.  It will take the light sensor reading from a phone running sensingkit (i.e a phone with the databox app installed), and it will move the pointer in a dial in response to changing readings.  Before you start, make sure you are logged in to the sdk, by going to [sdkurl]/login.  If you are not logged in you will be unable to save your work.  The finished app can be found by clicking on the <i>examples</i> menu item on the sdk toolbar and selecting: **databox.tutorial-light-gauge**

#### 1. connect the nodes together

Connect the sensing kit node (yellow datasource) to the uibuilder node (blue processor) to the app output node (orange output).  So data will flow from sensingkit, will be turned into a visualisation and then displayed on a screen in the app.

<figure class="figure">
  <img src="/images/tutorial/gauge/step1.svg" class="thumbnail" width="50%" alt="databox sdk">
  <figcaption class="figure-caption text-center">step one: connect the nodes together</figcaption>
</figure>


#### 2. choose 'light' as the sensing type

Double click on the sensingkit node.  You will be presented with a dialogue:

<figure class="figure">
  <img src="/images/tutorial/gauge/sensingkitdialogue.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step two: choose sensingkit's light sensor</figcaption>
</figure>

Select 'light' (if not already selected) and **optionally** in the 'name' field, provide a name such as <i>light sensor</i>.  Note that when you click on close, the details about the sensor are displayed at the bottom.  The description gives handy info about the range of lux values that the sensor will output, under which conditions.

<figure class="figure">
  <img src="/images/tutorial/gauge/sensingkitdescription.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step two: lux output values</figcaption>
</figure>

#### 3. select graphics for visualisation

The final bit is to connect the light value to an object in a visualisation.  This is where the uibuilder node comes in.  Double click it and you will be faced with a blank canvas.  We've created a range of images that can be used in your visualisation.  Click on the <img src="/images/tutorial/gauge/librarybutton.png" style="display:inline-block; width: 30px"> image (click it agaion to toggle the image library):

<figure class="figure">
  <img src="/images/tutorial/gauge/uibuilderblank.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: uibuilder</figcaption>
</figure>

Now drag the gauge and the pointer image onto the center of the canvas.

<figure class="figure">
  <img src="/images/tutorial/gauge/uibuildergauge.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: add artwork</figcaption>
</figure>

#### 4. attach data inputs to the visualisation

The uibuilder node has a notion of 'mappings' which is where we can connect data to elements of our graphics.  You'll see, when you select any objcet in the uibuilder canvas, that top right-hand side of the screen  will highlight the element that you have selected.  The two elements that you have dragged into the canvas are compound elements known as **groups** as they are composed of a bunch of other elements.  Click on the gauge pointer (as in the image below):

<figure class="figure">
  <img src="/images/tutorial/gauge/uibuildergaugepointer.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: add artwork</figcaption>
</figure>

We want to create a mapping between the light lux reading and the rotation of the pointer.  Click on the 'mapping' menu item on the right hand part of the screen.   You should see that you have selected a group and that the sensingkit source is under 'sources'.  Click on sensingkit and it will show you all of the data attributes that are sent in a message from the sensingkit light sensor.  We are interested in the 'value' item in the message payload, as this contains the lux value.  Click on that, then click on 'rotate', since we want to rotate the gauge pointer based on 'value'.

<figure class="figure">
  <img src="/images/tutorial/gauge/uibuildermapper.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step four: map 'value' to 'rotate'</figcaption>
</figure>

Once you have done this, you should see that a 'transformer' has been created.  A transformer is a function that takes the value you select in the sources and turns it into (in this case) a rotate value.  Click on the transformer to take a look what's there.

<figure class="figure">
  <img src="/images/tutorial/gauge/transformerdialogue.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step four: transformer dialogue</figcaption>
</figure>

There's quite a bit of info to process here.  At the top is a summary of all of the data that you have access to in your transformer function.  Note that one of those items is called 'value'.  You'll also see that the transformer states that the output from the function needs to be a 'transform string'.  This is a string of the form rotate(n) where n is the number of degrees that we want to rotate.  The current value:

```javascript
return `rotate(${value%360})`
```

Will just rotate the value mod 360 (i.e it will turn any numeric value to a number from 0 to 360).

Let's test what we have so far:

#### 4. test what we have so far

Click on ok on the uibuilder window.  Now click on test. This will pull up a menu on the right hand side of the screen.  You should see the app output icon.  When you click on that, a new test page will open.  Note that there will be a small delay before you see anything because in the background a new docker container is being built and launched on the server with your app code.

<figure class="figure">
  <img src="/images/tutorial/gauge/test.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step four: test</figcaption>
</figure>

Eventually you should see your gauge with the pointer rotating seemingly randomly.  The test page is sending mock light data to your app, which is causing the dial to rotate.

<figure class="figure">
  <img src="/images/tutorial/gauge/testoutput.png" width="50%" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step four: test output</figcaption>
</figure>

#### 5. adjust mapping

So now that we have a basic app doing something, we need to make th dial respond properly to lux values.  Lets say that we only want to use the top half of the dial - i.e. we want to rotate to -90 degrees for the lowest possible light reading and 90 degrees to the highest possible light reading (which, when we looked at the light sensor details, was 100000 for a very bright day).

Double click on the uibuilder node and click on the gauge pointer.  Now select the 'mapping' menu item and scroll down to the current transformer.  Click it and replace the code with the following:

```javascript
var rotation = -90 + parseInt((value/100000) * 180)
return `rotate(${rotation})`
```

So we're scaling the light value to a number between 0 and 1 (by dividing by the max value, 100000) and multiplying by 180 to get a value between 0 and 180.  We're then adjusting this by 90 degrees anticlockwise.  

<figure class="figure">
  <img src="/images/tutorial/gauge/transformerdialogue2.png" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">step five: adjust transformer</figcaption>
</figure>

Click on ok in the transformer window and ok on the uibuilder window. Now click the 'test' menu item and click on the test app again.  You should now see that the pointer only rotates within the top part of the gauge, providing a nice representation of the current light reading. 



