---
layout: base
title: databox sdk primer
---

The SDK is a visual coding environment for building <a href="http://databoxproject.uk" target="_blank">databox</a> apps.  All you need to get started is a github account.  You can then login at <a href="https://sdk.iotdatabox.com" target="_blank">https://sdk.iotdatabox.com</a> to start building apps.  This page provides a brief overview of the SDK, and will link to more detail where relevant.  We have created a set of [tasks](/g54ena/tasks) which involve building databox apps.  You do not have to go through these sequentially, and we have grouped them into tasks that require NO programming, and tasks that assume (basic) programming proficiency.  Please feel free to ignore these suggestions and build your own apps.

### A quick primer

The SDK is a visual coding environment that requires you to connect together 'nodes' into 'flows' to create an app.  Nodes are small black boxes of functionality.  Aside from a couple of 'special' nodes, they will either be *datastores* (things that create data e.g. twitter, output from a smart plug), *processors* (things that operate on data, e.g. format it for display, filter out items) or *outputs* (things that do something with data e.g turn on a bulb).   Typically a flow will consist of one or more datastores connected to one or more processors, connected to one or more outputs: 

<figure class="figure">
  <img src="/images/tutorial/gauge/step1.svg" class="thumbnail" width="50%" alt="example flow">
  <figcaption class="figure-caption text-center">example flow</figcaption>
</figure>

An app can be tested at any time during its creation.  Once finished, it can be published, after which it can be run on a databox.

#### Your first flow

To get started, login at <a href="https://sdk.iotdatabox.com" target="_blank">https://sdk.iotdatabox.com</a>.  Once logged in, you will be presented with a palette of nodes down the left hand side of the screen and a grey canvas.  Drag the **sensingkit** datasource onto the main canvas.  Now drag the **debugger** node onto the canvas and connect your datasource output to the debugger input.  That's it.  You have created your first flow.  All that the debugger node does is display the data that it receives.  

To test the output, click on TEST on the top blue toolbar.  This will build the app and run it in a test environment.  After a short while, you should see the debugger node appear on a sidebar on the right hand side.  Click on it and it will open a new tab with the debugger output.  If you go back to the SDK screen and double click on the sensingkit node, you'll see that there are a variety of sensors that you can choose.  Select a different sensor, then click on TEST, and you should see data with a different format from before.

#### Modifying your first flow

Let's modify your flow again.  Delete the connection between sensingkit and the debuger.  Now drag in the **chartify** node and the **app** node.  Connect the sensingkit to the chartify node to the app node.  The app node simply displays information on the screen  - in this case it will display whatever comes out of the charifty node.  Double click the sensingkit and select the light source.  Now double click the chartify node.  You'll see a bunch of options.  For "type" click on gauge.  In the "chart sources" section at the bottom, we want to plot the value of the light source.  Select VALUE under the xvalues heading.  Click on OK, and you are all done.

Click test again, and you should now see that there is an app node in the right hand side sidebar.  Click on it.  This time it should display a gauge, with a circle that moves in response to the change in data.

### Next steps

This is all you need to get started playing with the SDK. Go [here](/gettingstarted/sdk) for a fuller overview. You'll see that there are a bunch of examples of apps that do other things - by all means load them up and take a look.  We have also provided a [summary of the nodes available](/g54ena/nodes) in the sdk.  You should have most information that you require to work through a list of [suggested apps](/g54ena/tasks).


