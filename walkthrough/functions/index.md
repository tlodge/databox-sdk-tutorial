---
layout: home
---

#### databox sdk functions (dbfunction)

Databox sdk function nodes (dbfunction) allow you to write javascript to process input data.  There are a few headline things that you need to know:

- values **returned** by functions are sent as messages. If you do not wish to send a message, simply return nothing.
- to send multiple outputs, you send an array (item at index 0 is sent on the first output, at index 1 on the second output and so on)
- you are able to import npm libraries.  When you subsequently test a function a new container is built with any imported libraries installed.
- functions can store and access data to use between invocations using a  **context** object:
