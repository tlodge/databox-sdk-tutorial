---
layout: home
---


## sdk overview

<figure class="figure">
  <img src="/images/workflow.svg" class="img-fit-contain" alt="databox sdk">
  <figcaption class="figure-caption text-center">databox app workflow</figcaption>
</figure>



What follows is an overview of the sdk, and the features it provides for app development.  It is worth noting from the outset that the SDK is no silver bullet; it is well suited to building lightweight apps that operate on data to perform actuation or data visualisation; more complex apps (e.g. those that require significant user interaction, or complex data processing) will inevitably require developers to fall back to text editors and raw code; there are good examples of databox apps written in a variety of languages at the main [databox repo](https://github.com/me-box)

### anatomy of a databox app

There isn't all that much to a databox app.  It is simply:

1. some executable code that interacts with components on a databox to perform a task.
2. a manifest file that describes the app and specifies the datastores that it requires access to.

A datasource is anything that creates data e.g: iot devices such as smartplugs or bulbs, social media data feeds, system logs, webcam images and so on.  
We are not presecriptive about the language that an app is written in, only that it conforms to the databox apis for registering with the system and reading and writing from/to datastores.  All databox apps are run inside docker containers connected to a network that appropriately restricts interaction with other databox components.  

The  end-to-end databox app workflow process can be broken down into several stages:


The SDK is principally concerned with the first 5 i.e:

1. Write the app
2. Test the app
3. Create a manifest file to describe the app
4. Construct put the app in a docker container
5. Publish the app to a databox app store

The purpose of the databox SDK is to streamline each of these stages to get you building and deploying apps as efficiently as possible.   


### the anatomy of an sdk-built app

If you have not yet read the overview of the databox, it may be worth doing so before continuing.  Apps built in the SDK is loosely modelled on flow-based programming.  Apps are built as directed graph of black boxes with well-defined input and output interfaces (ports) connected by edges. We are principally concerned with data flow; data (information packets) flows along edges, in and out of nodes and is processed and modified along the way.  There are 3 main types of node that you'll work with: 

 - datasources 
 - processors  
 - outputs  

 Data sources map directly to their databox counterparts (i.e: originators of data i.e. iot devices such as smartplugs or bulbs, social media data feeds, system logs, webcam images and so on).  

 Processors are nodes that operate on data (e.g filtering, extracting, formatting, transcoding, reducing etc.). The most general processor node is a 'function' node which can be used to run abitrary javascript on input data. Processing nodes may have more than one output.   

 Outputs are the endpoints of a flow, they with typically perform some kind of actuation (turn a bulb on, send a tweet) or display (present a visualisation, graph etc).   

All nodes in the SDK provide interfaces for configuration - these can be very rich, and may operate as comprehensive tools in their own right.   For example the 'uibuilder' processing node provides a vector-based graphs tool for attaching incoming data to components of an svg image.  Nodes also come with comprehensive help; perhaps the most important is an overview of the data schemas that they expect and/or output.   

All code developed in the SDK is in Javascript, executed in nodejs. 

### testing an app

The databox sdk provides mock data to test apps against during the development process.  When you test a flow, all input data sources will emit this test data, and, where possible, you will be able to inpect simulated output (for example the 'bulb' output node will show a webpage with a bulb that will turn on or off in response to data). The databox sdk also provides a 'debug' node which is crucial for testing an app prior to publication.  The outputs from all nodes in a flow can be hooked up to a debug node to inspect output data, which can be paused and restarted at any time.


