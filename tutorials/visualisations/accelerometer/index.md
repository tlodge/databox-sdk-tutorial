---
layout: tutorial
image: /images/tutorial/bulb/bulb.svg
datasources: sensingkit
coding: a little
skills: building a visulisation, programatic creation of elements
title: tutorial - accelerometer vapour trail
duration: 20 minutes
---

This tutorial will guide you through more advanced features of the uibuilder node. The finished app can be found by clicking on the <i>examples</i> menu item on the sdk toolbar and selecting: **databox.tutorial-accelerometer-axes**. The app will move two circles in response to the amplitude of the x and y components from the accelerometer sensor in sensingkit.  The position, radius and opacity of the circles will change in response to the amplitude and a "vapour trail" will be created from older readings.

#### 1. connect the nodes together

As ever, the best way to start building our app is to connect the nodes together. We will be using the **sensingkit** accelerometer datasource.  We want to create circles whose centers and radii are dependent on the to the x and y values from the accelerometer (we can do this using the **uibuilder**)   Finally we want to output our visualisation on a screen, so we connect up the app node.  Once connected up, you should have a flow as follows:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/accelerometer/flow.svg"  width="50%" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step one: connect the nodes together</figcaption>
</figure>


#### 2. add the nodes

We now need configure each node to do the work. Double click the sensingkit node and set the sensor type to the accelerometer. Click on ok.  Note that when you select the sensingkit node it will give you information about the data that it emits.  It states that the maximum values for the X,Y and Z components is **38**.  

The grunt work will be done by the uibuilder, so double click to open it up.  We want two circles that move in response to the X and Y components of the accelerometer output.  Drag two circles from the palette onto the canvas.  Click on one circle and set its fill colour to red.  Click on the other and set its fill colour to blue.  Give the red circle the label "yaxis" and the blue circle the label "xaxis":

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/accelerometer/step1.png"  alt="add a red and a blue circle">
  <figcaption class="figure-caption text-center">add a red and a blue circle</figcaption>
</figure>

#### 3. make the circles move right across the screen

Over time, we want our circles to move from left to right across the screen, wrapping round when they get to the edge.  For each new item of data, we want to move the circle right.  Click on any circle.  Click on "mappings".  Lets map the sensingkit's ts value to the circle's cx value.

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/accelerometer/step2.png"  alt="mapper: map sensingkit ts to circle cx">
  <figcaption class="figure-caption text-center">mapper: map sensingkit ts to circle cx</figcaption>
</figure>

Once we have created this mapping, we should see a new transformer: sensingkit:ts -> xaxis:cx  or sensingkit:ts -> yaxis:cx.  Click on that transformer and it will open a dialogue.  Currently our mapping says that we want the cx (center x position of the circle) to map to the incoming timestamp (which is a unix timestamp).  This won't be very useful, as it will set the central point of the circle way off the screen (i.e. it will set cx to a value such as 150833664000).  Instead, what we want to do is to move the circle a constant amount with each "tick" of data.  Fortunately, all transformer functions pass in a value, <i>i</i> which is incremented with each new item of data.  It also passes in <i>h</i> and <i>w</i> which are the current height and width of the screen respectively.  Using these variables we can set the position of the circle to:

```javascript
return (i*10) % w
```

i.e the current index (0,1,2,3 etc) multiplied by a constant (10) modulus the width of the screen (so it wraps).  This will mean that now, with each new item of data, the circle will move 10 pixels to the right:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/accelerometer/step3.png"  alt="update transformer">
  <figcaption class="figure-caption text-center">update transformer</figcaption>
</figure>

We can do exactly the same for the other circle.  By the end you should be left with two transformers with identical formulas.  

#### 4. change width and opacity and y values of circles in response to x and y amplitude

Following a similar process as before, we now want to add mappings that will change other attributes of the circles in response to the sensor data.  

We want to move the circles into the center of the screen when the amplitude of the x or y sensor reading is at a maximum (which is roughly 38, as we saw when we configured the sensingkit node). Let's create a new mapping for the yaxis circle.  Click on the yaxis circle, then click on mapper, then select the sensingkit <i>Y</i> source and the <i>cy</i> attribute.  Click on the newly created transformer and add the following:

```javascript
const value = 38 + y;
return Math.round( (1-value/76) * h)
```  

Here we are simply shifting the range from [-38:38] to [0:76] then mapping the amplitude of y to the range (0-h) for the circle's cy, where h is the height of the screen, i.e. as the amplitude increases the circle moves from the top of the screen to the bottom.

Let's do something similar for the xaxis circle.   Select the xaxis circle and select X and cy.  This time we want the circle to move from h to 0 as amplitude increases (i.e from the bottom of the screen to the top):

```javascript
const value = 38 + x;
return Math.round( (1-value/76) * h)
```


Setting up the change in opacity and radius is easier.  Again, for each of the circles, create mappings from Y (for the yaxis circle) and X (for the xaxis circle) to opacity and radius.  For the opacity transformer, you need the following for yaxis:

```javascript
const value = 38 + y;
return value/76 * 1.0
```

and for the xaxis:

```javascript
const value = 38 + x;
return value/76 * 1.0
```


And for the radius for the yaxis:

```javascript
const value = 38 + y;
return  Math.round(50 * value/76)
```

and for the xaxis

```javascript
const value = 38 + y;
return  Math.round(50 * value/76)
```

i.e  set the radius from 0 to 50 pixels.

When you have finished you should have set up 8 transformers.  Yes, it is annoying having to re-align the range each time (i.e. const value = 38 + y, const value = 38 + x), and it would be better to simply adjust the range of the accelerometer before passing it into the uibuilder node.  This is easily done with a **dbfunction** node but we have kept this out of this tutorial for simplicity - you can see how this could be done in the [trump tutorial](/tutorials/visualisations/trump)


#### 5. testing our app

Let's test our app to see how it looks.  Click on OK.  Then click test.  Once the container is built you can click on the app node icon.  You should see your circles move across the screen from left to right, changing in radius and opacity and y position.

#### 6. adding 'vapour trails'

One important feature of the uibuilder that we have not yet explored is the 'lifetime' of our objects.  Once we have created an object, what happens if we want to create another one (with the same attributes) when the data changes in some way?  Consider a sensor that provides five temperature readings (t1,t2,t3,t4,t5), for 5 different parts of the house.  Each sensor will have a name ("t1","t2","t3","t4","t5").  Lets say we want a simple visualisation that moves a circle up or down based on a temperature reading.  So one way we could do this is to create 5 circles in uibuilder and then map one circle to t1's temperature reading, another to t2's temperature reading and so on. It's a bit laborious.  It would be much nicer if we could create a 'generic' circle that changes position according to a temperature and then tell uibuilder to clone this circle as needed. So in this case create a new circle whenever a sensor with a different name sends data i.e when "t1" sends its first data, clone the circle, when "t2" sends its first data, clone another circle and so on.

This is perhaps easier to understand by example.  uibuilder has a concept of **birth** and **death**. Click on any of your transformers (under the mappings tab) that modify an attribute of the yaxis circle (i.e sensingkit:ts->yaxis:cx, sensingkit:ts->yaxis:cy,sensingkit:ts->yaxis:r,sensingkit:ts->yaxis:opacity).  Up until now, all we have done is modify the code under the 'transformer' tab, but there is also  a "birth" and "death" tab. Click on the "birth" tab, and you are given three options "bind to key", "bind to function" and "reset".  Click on "bind to key", now select "TS".  We are telling uibuilder that whenever it sees a new "ts" value (which it will with every new data item), rather than modify the current circle, clone a new one.  Lets try this and see what happens.  Click on OK to save the change, then ok on the uibuilder.  Now click on test and wait for the container to build.  Now when you click on the app icon to see the test data, you should see something like:


<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/accelerometer/step4.png"  alt="update yaxis lifetime">
  <figcaption class="figure-caption text-center">update yaxis lifetime</figcaption>
</figure>

So a new yaxis circle is created with every new timestamp, whereas the xaxis circle behaves as before.  This looks nice, but creates a load of circles.  We want to clean up old ones.  We can do this by setting the death options.  The death options is a function that is evaluated with every new item of data received.  Click back to any of the yaxis transformers and now click on "Death". The Death function gets passed in the current source data for the mapping and must returns true if the object should be removed, and false otherwise.  Set the death function to:

```javascript
return (Date.now() - node.ts) > 2000 
```

i.e. remove the node if it is older than a couple of seconds.  This might not look like much against the test data, but will look better when data is arriving much faster.  This is what will create the vapour trail effect.  To create the same for the xaxis circle, repeat the steps above (i.e bind to the ts key for the birth options, and add in the code to the death options.

That's it.  Lots covered in this tutorial, but have a play with it and to familiarise yourself with object births and deaths.
