---
layout: base
title: sdk dev wishlist
---

The SDK is still very much in its infancy.  The following is a list of dev that we'd like to look at.  Please speaks to us if you'd like to get involved!

- **More processing nodes**

You still need a reasonable amount of coding abilility to do anything uswful with the SDK.  We'd like to add more nodes that can get users building decent apps with minimal/zero coding effort.  Nodes such as filters, range mappers, translators etc would be great.

- **Better type integration**

Having nodes able to describe the type of data that they work with and output is a very useful feature, and is a crucial part of what makes nodes such as the uibuilder work.  However it's very limited and doesn't work well with function (dbfunction) nodes.  One possibility is to move the execution environment code from javascript to a typed language (or something like Typescript)

- **Improvements to UIBuidler**

The UI Builder node helps users to build high quality visualisations, but there's much more that it could offer.  Other features we'd like to see are tweening, animations along paths, other output formats (e.g 3d/ canvas/ [VR](https://facebook.github.io/react-vr/])).

- **Better testing/ test data**

The test data from the mock data store is very limited.  We need to give developers much greater control over it for testing their apps.

- **SDK for drivers**

How/Can/Should the SDK be used to create drivers?  If so how?  

- **Historial data**

The SDK currently only deals with live data.  Need to support historical queries.

- **Better risk analysis/analytics**

The risk analysis in the SDK is little more than a placeholder.  Much more work needs to be done to try and create more useful/accurate risk ratings.

- **Code cleanup/refactoring**

The SDK code had grown/developed/changed to fit with new ideas as the databox project has evolved.  It will benefit from a restructuring/refactoring to make easier to navigate and use.  Other work required are decent tests / frontend performance analysis.  We'd also like to get rid of the reliance on brace (used for code editing) as it is a chunky library.  We also need to streamline/shrink/improve our css/sass code (it's a nasty mix of inline styles, old node red css and component specific scss/css imports).