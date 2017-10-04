---
layout: base
title: working with data
---

Given that databox apps will typically be operating on one or more sources of data there are a couple of features of the sdk that help you to keep track of the format of data as it moves through your app.  All nodes in a databox app are annotated with their data schema (using json-schema).  When you initially wire up an app, the sdk will do all it can to let you know the format of data flowing into a node, and the expected format of data flowing out of a node.   