---
layout: tutorial
image: /images/tutorial/gauge/gauge.svg
datasources: sensingkit
coding: none
skills: basic visualisation
title: light gauge tutorial
duration: 10 minutes
---

This tutorial will show you how to build a simple light monitor.  It will take the light sensor reading from a phone running sensingkit (i.e a phone with the databox app installed), and it will move the pointer in a dial in response to changing readings.  Before you start, make sure you are logged in to the sdk, by going to [sdkurl]/login.  If you are not logged in you will be unable to save your work.

#### 1. connect the nodes together

Connect the sensing kit node (yellow datasource) to the uibuilder node (blue processor) to the app output node (orange output).  So data will flow from sensingkit, will be turned into a visualisation and then displayed on a screen in the app.

<figure class="figure">
  <img src="/images/tutorial/gauge/step1.svg" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step one: connect the nodes together</figcaption>
</figure>


#### 2. choose 'light' as the sensing type

Double click on the sensingkit node.  You will be presented with a dialogue:

<figure class="figure">
  <img src="/images/tutorial/gauge/sensingkitdialogue.png" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step two: choose sensingkit's light sensor</figcaption>
</figure>

Select 'light' (if not already selected) and **optionally** in the 'name' field, provide a name such as <i>light sensor</i>.  Note that when you click on close, the details about the sensor are displayed at the bottom.  The description gives handy info about the range of values that teh sensor will output, under which conditions.

<figure class="figure">
  <img src="/images/tutorial/gauge/sensingkitdescription.png" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step two: lux output values</figcaption>
</figure>

#### 3. attach the outputs from the light sensor to a visualisation

We're almost done!  The final bit is to connect the light value to an object in a visualisation.  This is where the uibuilder node comes in.  Double click it and you will be faced with a blank canvas.  We've created a range of images that can be used in your visualisation.  Click on the <img src="/images/tutorial/gauge/librarybutton.png" style="display:inline-block; width: 30px"> image:

<figure class="figure">
  <img src="/images/tutorial/gauge/uibuilderblank.png" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: uibuilder</figcaption>
</figure>

Now drag the gauge and the pointer image onto the center of the canvas.

<figure class="figure">
  <img src="/images/tutorial/gauge/uibuildergauge.png" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: add artwork</figcaption>
</figure>

And add a mapping from value to rotation for the pointer

<figure class="figure">
  <img src="/images/tutorial/gauge/mapperpanel.png" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: map value to rotation</figcaption>
</figure>

Now run a test to see what happens


<figure class="figure">
  <img src="/images/tutorial/gauge/transformerdialogue.png" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">step three: adjust rotation</figcaption>
</figure>

what are the parameters passed in to the transformer?