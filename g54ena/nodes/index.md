---
layout: base
title: databox sdk nodes
---

The following is a quick summary of all of the nodes in the SDK and what you might use them for:

<table>
  <thead>
    <tr>
      <th>name</th>
      <th>node</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    {% for node in site.data.nodes %}
    <tr>
      <td><img class="thumbnail" src="{{ node.image }}" alt="{{ node.name }}"></td>
      <td>{{ node.name }}</td>
      <td>{{ node.use }}</td>
      <td>{{ node.description }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>