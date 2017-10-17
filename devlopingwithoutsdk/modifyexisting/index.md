---
layout: base
title:  developing without the sdk
---

Building app with the SDK can be quick and fun. However, it has a number of limitations. For example,

 - The final app will be built on NodeJS which produces large images and can be memory inefficient
 - You currently can't build drivers
 - Some data sources aren't supported in the SDK

To overcome these limitations it is possible to develop apps outside of the SDK.  this guide will give you an introduction to doing so.  to explain how to do this we will add it currently existing Databox Apps.

#### Getting the source code

Once you have in installed Databox as described [here](/gettingstarted/install) you can you the 'databox-install-component' command to locally install and build the image for apps or drivers published on GitHub. Run this command in your Databox root folder to install app-os-monitor.


```
./databox-install-component me-box/app-os-monitor
```

This will:
  1. pull the source code for the app-os-monitor from Github to your machine
  2. build and tag the downloaded code into a docker image
  3. upload the databox-manifest.json to the local app store

> Note: if you are starting a new app then you can manually create a folder. As a minimum, you will need a Dockerfile and a databox-manifest.json to be able to install the app/driver.
> Note: if you want to modify this component fork it on GitHub fist the use `./databox-install-component [YOUR_USERNAME]/app-os-monitor` once you have made an tested your changes then you can submit a pull request back to the original repository

Once this command has completed you can edit the code in ./app-os-monitor to make your changes.

#### Checking the app is available locally

Now that you have installed app-os-monitor locally it is available from the remote an local app-server. When you go back into the databox UI and install  app-os-monitor there will be a drop down next to the install button which allows you to select the required store.

> Note: If you are developing an app/driver only available locally then there will be no option.

Install the local version and confirm it works by accessing its UI (you will need to install driver-os-monitor first).

You can confirm the Databox is running you local image by:

```
./docker service ls
```

The output should like this notice the missing (databoxsystems/):

```
ID                  NAME                        MODE                REPLICAS            IMAGE
hwrajzssotmh        app-os-monitor              replicated          1/1                 app-os-monitor
zmv1nk7jojd3        databox_arbiter             replicated          1/1                 databoxsystems/arbiter:latest
o3i0okog00e2        databox_container-manager   replicated          1/1                 databoxsystems/container-manager:latest
j4ktcn8kyt8y        databox_export-service      replicated          1/1                 databoxsystems/export-service:latest
```

#### Making a changes

Open the apps src code in the editor of your choice and make the required changes and save them! Once this has been done you can run  `./databox-install-component` again to rebuild the image or:

```
cd [SRC-FOLDER]
docker build -t [APP-NAME] .
```

Then you can go back into the databox UI and restart the app using the refresh button on the app list screen. This works for drivers too.

>Note: This is a quick way to get started but sometimes using a different approach is needed see [docker-dev.md](https://github.com/me-box/documents/blob/master/guides/docker-dev.md)

#### Debugging problems

Docker service logs is your friend, all apps driver and stores are run as docker services so use:

```
docker services logs app-os-monitor -f
```

To stream the logs form your modified app.