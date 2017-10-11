---
layout: base
title: databox overview
---

The Databox envisions an open-source personal networked device, augmented by cloud-hosted services, that collates, curates, and mediates access to an individual’s personal data by verified and audited third party applications and services.   The Databox will form the heart of an individual’s personal data processing ecosystem, providing a platform for managing secure access to data and enabling authorised third parties to provide the owner with authenticated services, including services that may be accessed while roaming outside the home environment.

### The databox architecture

The following is an overview of the databox architecture.  

<figure class="figure">
  <img src="/images/overview/databoxoverview.svg" class="thumbnail" width="80%" alt="databox high-level architecture">
  <figcaption class="figure-caption text-center">databox high-level architecture</figcaption>
</figure>

Perhaps the most important features to become familiar with are **datasources**, **drivers** and **datastores**.  A datasource is either some physical hardware (such as a sensor, a device in the home, e.g. Philips Hue Bulbs, smartplugs) or a cloud service (e.g. Twitter, Facebook, Gmail).  In order for the databox to communicate with a datasource, it needs a **driver**.  A driver is a piece of software that is installed on the databox to communicate with a specific datasource, therefore, each datasource must have a databox driver in order to work with the databox.   Drivers will write data to a **datastore**, and apps that have the appropriate permissions can then get access to data in the datastore.  Apps may also write to a datastore in order to actuate a datasource (e.g. turn a bulb on).  The driver will send an actuatuion request to a datasource when an appropriate request is written into its datastore.

Apps, therefore, do not have direct access to drivers; all they know about is datastores.  The **arbiter** is the component that will grant permissions for apps to access particular datastores. All apps have a **manifest** file, which sets out the datasources it will require access to.  At install time, if the user accepts the details of the manifest, then the arbiter will set up the necessary permissions.

All components in the databox run as docker containers, and it is the **container manager's** job to pull, run and manage these containers. 

 


