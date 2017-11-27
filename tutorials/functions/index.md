---
layout: base
title: function tutorials
---

This section provides details on using the **dbfunction** (databox functon) node.  The dbfunction node allows you to write javascript code to process data and unlike other nodes, it is relatively unconstrained. 

There are a few headline things that you need to know:

- values **returned** by functions are sent as messages. If you do not wish to send a message, simply return nothing.
- to send multiple outputs, you return an array (item at index 0 is sent on the first output, at index 1 on the second output and so on), and explicitly set the number of outputs in the outputs dropdown (currently limited to 5).
- you are able to import npm libraries.  When you subsequently test a function a new container is built with any imported libraries installed.
- functions can store and access data to use between invocations using a  **context** object:

```javascript
//store foo
context.set("foo", myvalue)

//retrieve foo
var myvalue = context.get("foo") || adefaultvalue
``` 

- Several nodes need to know the 'shape' of data that they are receiving as input (e.g. uibuilder).  If the function node sends data to one of these nodes, then it has to specify its schema.   The node will try and do this automatically, but you may need to add further detail.

- If you connect the input and output nodes to a dbfunction before you write code, you can get the node to create skeleton code to ensure that the inputs and outputs conform to what is expected.

The following tutorials make use of functions in some way:

<table>
  <thead>
    <tr>
      <th>tutorial</th>
      <th>description</th>
      <th>example name in sdk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="/functions/bulb">flash bulbs</a></td>
      <td>this turns a bulb on then off each second.  It makes use of the **context** object to store state between the receipt of new data</td>
      <td>databox.tutorial-on-off</td>
    </tr>
    <tr>
      <td>shake light</td>
      <td>this takes the sensingkit accelerometer x data and turns a bulb on or off when it hits a threshold value </td>
      <td>databox.tutorial-shake-light</td>
    </tr>
    <tr>
      <td>binary count</td>
      <td>this uses the **context** object and has multiple outputs </td>
      <td>databox.tutorial-hue-binary</td>
    </tr>
  </tbody>
</table>