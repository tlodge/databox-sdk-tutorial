---
layout: base
title: datasources, processors and outputs
---

Out of the box the sdk gives you several 'nodes' that you can use to construct your apps. 

- Datasources

Will typically just have a single output on which they send data.  Data sources may create different data depending on how they are configured.  For example the sensingkit datasource can be configured to to emit data for a range of onboard sensors, including accelerometer, light, audio and bluetooth scans.  The data schema will vary according to the specifics of how a datasource is configured.

- Processors

Act upon data, usually to transform it in some way.  For example the 'chartify' processor will take input data and formatready for rendering a chart.  The 'extract' processor will extract a set of attributes from data.  The most general-purpose processor is a dbfunction (databox function), which allows a developer to write javascript code and import npm libraries to process data.  We provide much more information on writing dbfunctions [here](/walkthrough/functions)

- Outputs

 These are typically nodes at the end of a flow; they perform some kind of effect, such as actuation, visualisation or communication.  We currently support a limited set of output nodes; anything that needs to output data (charts, visulisations, html, text) will use the 'app' node.  If you want to actuate [philips hue bulbs](https://www.philips.co.uk/c-m-li/hue), you can use the bulbsout node, and if you want to turn smart plugs on/off you can use the plugout output which works with [tplink smart plugs](http://uk.tp-link.com/products/details/cat-5258_HS100.html).


 There are also a couple of special nodes that do not fit into the categories above:

 - inject

 This most closely resembles a datastore; it can be use to one-off or peridoic events, perhaps to kick start an app or undertake a periodic task.

 - debugger

 This is a node that is used during testing; it allows a developer to inspect the data output from a node; the all debugger nodes are automatically stripped out when an app is published.