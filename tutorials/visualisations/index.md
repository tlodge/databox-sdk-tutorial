---
layout: base
title: visualisation tutorials
---

This set of tutorials will take you through the tools for building visualisations.  Theer are several nodes that allow you to present data graphically:

- Chartify
- Listify
- Webify
- UIBuilder


All of these can be hooked directly to the **app** node which will present the visualisations in the databox dashboard.  Note that if you want to create svg-based visualisations using the UIBuilder, we'd recommend using a graphics package such as [Inkscape](https://inkscape.org/) or [Affinity Designer](https://affinity.serif.com).

<table>
  <thead>
    <tr>
      <th>tutorial</th>
      <th>node used</th>
      <th>description</th>
      <th>example name in sdk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="/gettingstarted/sdk">freememory</a></td>
      <td>chartify</td>
      <td>this takes the number of bytes free from the osmonitor node and displays it on a bar chart</td>
      <td>databox.tutorial-freememory</td>
    </tr>
    <tr>
      <td><a href="/tutorials/visualisations/gauge">light gauge</a></td>
      <td>uibuilder</td>
      <td>this takes the light reading from sensingkit and renders the value on a svg gauge </td>
      <td>databox.tutorial-light-gauge</td>
    </tr>
    <tr>
      <td><a href="/tutorials/visualisations/trump">trump clock</a></td>
      <td>uibuilder</td>
      <td>this renders a doomsday clock whose values change based on the sentiment score from tweets</td>
      <td>databox.tutorial-trump</td>
    </tr>
    <tr>
      <td><a href="/tutorials/visualisations/accelerometer">accelerometer trail</a></td>
      <td>uibuilder</td>
      <td>this renders the x and y values of an acclerometer as over time.  It uses more advanced uibuilder features </td>
      <td>databox.tutorial-accelerometer-axes</td>
    </tr>
  </tbody>
</table>
