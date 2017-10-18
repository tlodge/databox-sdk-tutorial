---
layout: base
title: sdk overview
---

What follows is an overview of the sdk, and the features it provides for app development. If you have not yet read the overview of the databox, it may be worth doing so before continuing.  It is worth noting from the outset that the SDK is no silver bullet; it is well suited to building lightweight apps that operate on data to perform actuation or data visualisation; more complex apps (e.g. those that require significant user interaction, or complex data processing) will inevitably require developers to fall back to code; there are good examples of databox apps written in a variety of languages at the main [databox repo](https://github.com/me-box)

### the anatomy of a databox app

There isn't all that much to a databox app.  It is simply:

1. some executable code that interacts with (datastores)[/overview/databox] on a databox to perform a task.
2. a manifest file that describes the app and specifies the datastores that it requires access to.

All databox apps are run inside docker containers connected to a network that appropriately restricts interaction with other databox components. A datastore is the primary mechanism by which an app communicates with a datasource.  A datastore is both a (i) repository of data from a datasource, and (ii) an endpoint for performing actuation.  All communication with a datastore is through an API.  We are not prescriptive about the language that an app is written in, only that it uses the databox APIs for registering with the system and reading and writing from/to datastores.   Currently we have libraries that simplify calls to the API written for [nodejs](https://github.com/me-box/node-databox), [python](https://github.com/me-box/lib-python-databox) and [go](https://github.com/me-box/lib-go-databox). 

### the anatomy of an sdk-built app

Apps built in the SDK is loosely modelled on flow-based programming.  Apps are built as directed graph of black boxes with well-defined input and output interfaces (ports) connected by edges. We are principally concerned with data flow; data (information packets) flows along edges, in and out of nodes and is processed and modified along the way.  There are 3 principle types of node that you'll work with: 

 - datastores
 - processors  
 - outputs  

SDK datastores differ slightly from the databox notion of a datastore in that they are **only** originators of data; they do not perform actuation - this is performed by output nodes.

Processors are nodes that operate on data (e.g filtering, extracting, formatting, transcoding, reducing etc.). The most general processor node is a 'function' node which can be used to run abitrary javascript on input data. Processing nodes may have more than one output.   

Outputs are the endpoints of a flow, they with typically perform some kind of actuation (turn a bulb on, send a tweet) or display (present a visualisation, graph etc).   

All nodes in the SDK provide interfaces for configuration - these can be very rich, and may operate as comprehensive tools in their own right.   For example the 'uibuilder' processing node provides a vector-based graphs tool for attaching incoming data to components of an svg image.  All nodes also come with comprehensive help; perhaps the most important is an overview of the data schemas that they expect and/or output.   

All code developed in the SDK is in Javascript, executed in nodejs. 

### app development workflow

The  end-to-end databox app workflow process can be broken down into several stages:

<figure class="figure">
  <img src="/images/overview/workflow.svg" class="thumbnail" alt="databox sdk">
  <figcaption class="figure-caption text-center">databox app workflow</figcaption>
</figure>

The SDK is principally concerned with the first 5 i.e:

1. Write the app
2. Test the app
3. Create a manifest file to describe the app
4. Construct put the app in a docker container
5. Publish the app to a databox app store


The purpose of the databox SDK is to streamline each of these stages to get you building and deploying apps as efficiently as possible.   The databox [dashboard](/gettingstarted/dashboard) supports stages 6-9.

