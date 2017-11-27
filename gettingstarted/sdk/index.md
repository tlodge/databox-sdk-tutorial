---
layout: base
title: a first look at the sdk
---

This section assumes that you have already installed the sdk using [these](/gettingstarted/install) instructions, or that you are accessing it through the <a href="https://sdk.iotdatabox.com" target="_blank">cloud version</a> (opens in new tab).  It will take you though loading up a simple example app, testing it and then publishing it to the app store.

Before you begin, if you do not yet have a github account, you can sign up [here](https://github.com/join).

### Login

If you have installed the SDK locally, go to: <a href="http://127.0.0.1:8086" target="_blank">http://127.0.0.1:8086</a> (opens in new tab).  Else go to the<a href="https://sdk.iotdatabox.com" target="_blank">cloud version</a> (opens in new tab).  You will be presented with a login screen.  

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/sdklogin.png" width="50%" alt="sdk login page">
  <figcaption class="figure-caption text-center">sdk login page</figcaption>
</figure>

Click on "login with github", review the requested permissions and accept them if you are happy.  You should now be logged in to the sdk workspace. 

### The SDK workspace

Down the left hand side is the palette of 'nodes' that you can use to construct your databox app.  They are separated into datasources (in yellow), processors (in blue) and outputs (in orange).

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/mainscreen.png" width="80%" alt="sdk main screen">
  <figcaption class="figure-caption text-center">sdk main screen</figcaption>
</figure>

If you have not yet read the overview of the databox, it may be worth doing so before continuing.  Apps built in the SDK use a (loose) flow-based programming paradigm.  Apps are built as a directed graph of black boxes with input and output interfaces (ports) connected by edges. We are principally concerned with data flow; data (information packets) flows along edges, in and out of nodes.  It is processed and modified along the way.  Out of the box the sdk gives you several 'node' types that you can use to construct your apps:

- datasources 

**Datasources** are originators of data (e.g. iot devices such as smartplugs or bulbs, social media data feeds, system logs, webcam images and so on).   They will typically have a single output on which they send data.  Data sources may create different data depending on how they are configured.  For example the sensingkit datasource can be configured to to emit data for a range of onboard sensors, including accelerometer, light, audio and bluetooth scans.  The data schema will vary according to the specifics of how a datasource is configured.

- processors  

**Processors** are nodes that operate on data (e.g filtering, extracting, formatting, transcoding, reducing etc.). The most general processor node is a 'function' node which can be used to run abitrary javascript on input data. Processing nodes may have more than one output.   

- outputs

**Outputs** are the endpoints of a flow, they will typically actuate (turn a bulb on, send a tweet) or display (present a visualisation, graph etc).  We currently support a limited set of output nodes; anything that needs to display data (charts, visualisations, html, text) will use the 'app' node.  If you want to actuate [Philips Hue Bulbs](https://www.philips.co.uk/c-m-li/hue), you can use the **bulbsout** node, and if you want to turn smart plugs on/off you can use the **plugout** output which works with [TPLink Smart Plugs](http://uk.tp-link.com/products/details/cat-5258_HS100.html).


There are also a couple of special nodes that do not fit into the categories above.  The **inject** node (in red) resembles a datastore; it can be used to generate one-off or peridoic events, perhaps to kick start an app or undertake a periodic task.

The **debugger** node is used during testing; it allows a developer to inspect the data output from a node; debugger nodes are automatically stripped out when an app is published.

All nodes in the SDK provide interfaces for configuration - these can be very rich, and may operate as comprehensive tools in their own right.   For example the 'uibuilder' processing node provides a vector-based graphics tool for attaching incoming data to components of an image.  Nodes also come with context-sensitive help; perhaps the most important is an overview of the data schemas that they expect and/or output.     

### Running an example app

Now let's load up an example app.  Each of the example apps correspond to tutorials in the SDK TUTORIAL section of this guide.  Click on EXAMPLES on the main toolbar, and you will be presented with a list.

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/examplerepos.png" width="30%" alt="example repos">
  <figcaption class="figure-caption text-center">example repos</figcaption>
</figure>

Click on the **databox.tutorial-freememory**.  This will open a new 4-node flow in the workspace.  By looking at the flow, it is already possible to get some idea of what the app does.  The yellow **osmonitor** node is feeding data into a **chart** (processor) node and a **debug** node.  Finally the chart node is feeding data into the app (output) node.  The app node is simply a display output; it will display data on a screen on the databox dashboard.

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/exampleflow.png" width="50%" alt="example flow">
  <figcaption class="figure-caption text-center">monitor chart flow</figcaption>
</figure>

Let's look more closely the osmonitor datasource (the yellow node).  Double click on it, and you will see a new dialogue pop up:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/configureosmon.png" alt="configure osmonitor node">
  <figcaption class="figure-caption text-center">configure osmonitor node</figcaption>
</figure>

This is a very simple dialogue, with only a few options.  All nodes can be given a 'name'; this is simply a convenience that helps you keep track of your nodes when a flow gets larger.  The osmonitor node also has a 'type' field.  When you click on it, you'll see that you have various options for the type of data that you are interested in.  Click on the 'free memory' type and perhaps give the node the name 'free memory'

Now let's look at the chart node; double click on the blue chart node.  This is a more complex dialogue.  

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/configurechart.png" alt="configure chart node">
  <figcaption class="figure-caption text-center">configure chart node</figcaption>
</figure>

The chart node takes incoming data and formats it for plotting a chart.  There are currently only two types of chart that are supported: Bar and Gauge.  The bar graph plots bars on an x/y axis, the gauge chart plots a single value along a semicircle.  We are interested in free memory over time, so leave the type as 'bar'.  At the bottom of the dialogue, under 'chart sources', you should see the osmonitor node, with an option to select the x-value and the y-value.  We want the x value to be the timestamp (ts), and the y-value to be the actual free memory value (value).  How do we know that ts means 'timestamp' and 'value' means the amount of free memory?  At the top of the dialogue there is a <i> there are one inputs to this function (click to view)</i>.  If you click on that, it provides information on the data that is coming from the osmonitor node; most importantly, the **payload** of the message is an object with a 'ts' and a 'value' field.

Once you have selected the x-value and y-value, click on OK.  Note that whenever you re-open this dialogue you will need to re-select what it is that you want the chart to display, as it does not know whether the inputs have changed and invalidated the current selection.

### Testing your app

We are now ready to test our app.  The output and debug node do not need any configuring (yet).  Click on TEST on the toolbar:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/testnodes.png" width="80%"  alt="test output">
  <figcaption class="figure-caption text-center">test output</figcaption>
</figure>

When you click on test, quite a bit happens behind the scenes; the server builds a new container with your app logic in it and runs it against mock data.  It then presents all of the outputs than can be inspected; in this case, the **debug** node and the **app** node.  Let's look at the debug node first.  Remember this is hooked up to show us all of the data being emitted from the **osmonitor** node:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/debugger.png" width="80%" alt="debugger output">
  <figcaption class="figure-caption text-center">debugger output</figcaption>
</figure>

The debugger will show you the payload of the messages that are being emitted from osmonitor.  If you want to see the entire object, you can double click on the debugger node and, for the SHOW field, select "full message", then click TEST again.  You can pause and restart messages in the debugger as appropriate (on the top left hand of the screen).  

Close the debugger tab, and now click on the app.  After a short delay, you should see bars emerge as new data arrives:


<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/charttest.png" width="80%" alt="chart visualisation">
  <figcaption class="figure-caption text-center">chart visualisation</figcaption>
</figure>

### Publishing your app

Before we publish the app, note how on the right hand side of the toolbar there are a couple of shields.  As you build your app, the SDK works out an overall 'risk' rating, based upon the nodes that you have used,.  To understand how it has arrived at this rating, you can click on the shields to get a breakdown.  Note that this is currently a very crude metric, and we are actively researching on how we might improve this.

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/risk.png" width="50%" alt="risk overview">
  <figcaption class="figure-caption text-center">risk overview</figcaption>
</figure>

You are now ready to publish, so click on PUBLISH on the toolbar.  It will pop up a dialogue:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/publishform.png" alt="publish form">
  <figcaption class="figure-caption text-center">publish form</figcaption>
</figure>

The entries that you put in here will be used to generate a (mainfest)[/overview/databox] file that will provide details to the user when the app is installed on a databox.  Once you have filled in the details (tags need to be a comma separated list).  Click on PUBLISH.  This can take some time, as the code is saved to your github repo, the container is built and pushed to the app store:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/publishing.png" alt="publishing your app">
  <figcaption class="figure-caption text-center">publishing your app</figcaption>
</figure>

Once done, your app should be ready to install on the databox!  You should also see that the code now lives in a new repo with the name of your app:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/newrepos.png" width="30%" alt="your new repo">
  <figcaption class="figure-caption text-center">your new repo</figcaption>
</figure>

If you go to your github account and you should see it there too.

To run your app on the databox, go to the [dashboard](/gettingstarted/dashboard) guide.