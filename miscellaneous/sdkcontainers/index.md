---
layout: base
title:  the sdk containers
---

There are a bunch of containers that the sdk uses, and this is a listing of what they are, what they do and where they can be found:

<table>
  <thead>
    <tr>
      <th>container</th>
      <th>repo</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
  	<tr>
      <td>tlodge/databox-sdk</td>
      <td><a href="https://github.com/me-box/platform-sdk">https://github.com/me-box/platform-sdk</a></td>
      <td>This is the sdk container, it serves up the dev environment and reads/wriets to github, appstore and registry as appropriate</td>
    </tr>
    <tr>
      <td>tlodge/databox-test-server</td>
      <td><a href="https://github.com/tlodge/databox-test-app">https://github.com/tlodge/databox-test-app</a></td>
      <td>This is the container that runs tests for the sdk. The base image is tlodge/databox-test-server-base.   Node-red instances connect to it to send data, which it then sends to a the client over websockets. </td>
    </tr>
    <tr>
      <td>tlodge/databox-datasource-mock</td>
      <td><a href="https://github.com/me-box/source-sdk-mock">https://github.com/me-box/source-sdk-mock</a></td>
      <td>This is the container that creates mock data for testing. The base image is tlodge/databox-datasource-mock-base.</td>
    </tr>
    <tr>
      <td>tlodge/databox-red</td>
      <td><a href="https://github.com/tlodge/databox-nodered-nodes">https://github.com/tlodge/databox-nodered-nodes</a></td>
      <td>This is the base images used to build TEST containers.  It is an instance of node-red alongside the nodes that are supported in the SDK.  The nodes can send messages to the databox-test-server over json-sockets can send messages to the client over websockets</td>
    </tr>
    <tr>
      <td>tlodge/databox-sdk-red</td>
      <td><a href="https://github.com/tlodge/node-red-app-webserver">https://github.com/tlodge/node-red-app-webserver</a></td>
      <td>This is the node-red execution environment and webserver that is used to create a databox app. Node-red nodes can communicate with the webserver over json-sockets, and the webserver then pushes messages to the client over websockets.  The base image is tlodge/node-red-app-webserver-base </td>
    </tr>
     <tr>
      <td>tlodge/databox-app-server</td>
      <td><a href="https://github.com/tlodge/db-app-server">https://github.com/tlodge/db-app-server</a></td>
      <td>Only used when running a cloud version of the sdk, and can be superceded by <a href="https://github.com/me-box/platform-app-server">https://github.com/me-box/platform-app-server</a></td>
    </tr>
    <tr>
      <td>tlodge/mongo</td>
      <td></td>
      <td>Mongo server for saving users</td>
    </tr>
     <tr>
      <td>tlodge/redis</td>
      <td></td>
      <td>redis server for persisting sessions</td>
    </tr>
  </tbody>
</table>
