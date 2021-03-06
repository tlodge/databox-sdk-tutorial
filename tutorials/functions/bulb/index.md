---
layout: tutorial
image: /images/tutorial/bulb/bulb.svg
datasources: sensingkit
coding: a little
skills: writing a simple function, actuation
title: tutorial - hue bulbs
duration: 10 minutes
---

This tutorial will show you how to write a simple function to turn a philips hue bulb on and off every second.  It will get you familiar with how functions work in the sdk.  The finished app can be found by clicking on the <i>examples</i> menu item on the sdk toolbar and selecting: **databox.tutorial-on-off**

#### 1. connect the nodes together

The best way to get started writing apps is to connect your nodes together as you expect the data to flow. We want to flash our bulbs every second,  so we want to use the red **inject** node to emit a message every second.  We want to turn that message into an instruction to turn the bulb on or off, so we connect the inject node to a **dbfunction** (databox function) node.  Finally we want to send that instruction to the bulb, so we connect to the **bulbsout** node.  It's always useful to check that the output from a function is as you expect, so we also connect the output from dbfunction to a **debug** node.  Once connected up, you should have a flow as follows:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/bulb/flow.svg" width="50%" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step one: connect the nodes together</figcaption>
</figure>


Now that this is connected up, we need configure each node to do the work.

#### 2. configure the nodes

We have said that we want to flash the bulb on/off every second.  Double click on the red inject node.  You are presented with a configuration dialogue.  We don't really care what kind of message the node sends, just that it sends one every second:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/bulb/inject.png" alt="configure the inject noder">
  <figcaption class="figure-caption text-center">step two: configure the inject node</figcaption>
</figure>

Select the repeat option as interval, and leave as the default (once every second).  Click on ok.  A timestamp message will be sent to the function node every second.

Now we need to make sure that the dbfunction node sends an on or off message each time it gets a message from the inject node.  Double click on your dbfunction node.  There's quite a bit of information to take in here.  Because you have connected up your nodes already, the function node is able to give you information about data coming in to this node and the data expected by the nodes that it is connected to.  We're interested in the format of the data expected by the bulbsout node.  Click on the <i>there are two recipients of data from this function (click to view)</i>.  Next to the bulb icon you'll see a table:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/bulb/bulbschema.png" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step two: configure the dbfunction node</figcaption>
</figure>

This tells us all we need to know about the format of the message that we need to send out from this function.  Note that to send a message from a function we just **return** it.  The schema is telling us that the bulbsout node expects an object with two attributes:  a type and a payload.  The type is a string that needs to be either either 'set-bulb-on', 'set-bulb-hue', 'set-bulb-brightness'.  The format of the payload is dependent on whatever 'type' is chosen.  If, for example, we were to choose 'set-bulb-on', our payload would need to be a string that was either an "on" or an "off".  We know that we want to set the bulb on or off. There are therefore two possible messages we might want to send:

```
//turn a bulb on:
{
	type: "set-bulb-on",
	payload: "on"
}
//turn a bulb off:
{
	type: "set-bulb-on",
	payload: "off"
}
``` 

So far so good.  However we want to alternate the message that we send, based on the current state of the bulb (i.e if it's off, send an "on", and if it's on, send an "off").  In order to do this, we need to have a little bit of state that persists between each input event.  To do this we make use of a special "context" object.  The context object allows you to store and retrieve data.  The data will persist for the duration that an app is running.  It is easy to use:

```
//store foo
context.set("foo", myvalue)

//retrieve foo
var myvalue = context.get("foo") || adefaultvalue
``` 

We now have all we need in order to write our on/off function:

```
//get the current state, and if it does not exist, set it to "on"
const state = context.get("state") ||  "on";

//update the state, if it was on, set to "off" otherwise set to "on"
context.set("state", state === "on" ? "off":"on");

//send our instruction to the bulb
return {				
  type:"set-bulb-on",
  payload: state,
}
```


Write this in the function block and click ok.

That's it.  You should now have a fully working databox app that will flash a hue bulb on or off.  


#### 3. testing our app

Lets convince ourselves that the app works as expected.  Remember that there are two outputs from our dbfunction: a debug node and a bulbsout node.  Click on TEST on the sdk editor toolbar.  This will trigger a test container to be built (on the server or your machine, depending on where the sdk is installed).  You should be presented with a debug and a app output node on the right hand side of the screen.  Lets look at what is being sent to the debug node:

<figure class="figure">
  <img class="thumbnail" src="/images/tutorial/bulb/bulbdebug.png" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step three:  check dbfunction output in debugger</figcaption>
</figure>


This looks pretty good.  We are seeing an alternating on or off message every second.  But wait - where is the 'type' bit of the message.  By default the debugger only shows the message payload.  To see the entire message, cdouble click the debug node and next to SHOW, select full message.  Now re-rerun the debugger, and you should see a fuller message:

<figure class="figure">
  <img src="/images/tutorial/bulb/bulbdebugfull.png" class="thumbnail" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step three:  check full dbfunction output in debugger</figcaption>
</figure>

Now you can see that the "type" is sent in the message along with a bunch of other parameters that are added by default to all messages.

Finally we can check to see what happens to our bulb when the app is run.  Obviously we are not connected up to a real bulb, but the sdk can simulate it.  Click on the bulb on the right of the screen.  You should see a bulb which alternates between yellow (on) and black (off).

<figure class="figure">
  <img src="/images/tutorial/bulb/bulbonoff.png" class="thumbnail" alt="connect the flows together">
  <figcaption class="figure-caption text-center">step three:  simulate the bulb </figcaption>
</figure>

