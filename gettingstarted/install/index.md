---
layout: base
title:  installing databox and the sdk
---


## Prerequisites

 These instructions will assume you are using a mac that is connected to the Internet, though the commands should translate directly to flavours of linux.  Before you get started you will need the following:

 - docker
 - git

 We also recommend that you install the databox dashboard app, which can be found on Google Play (and Apple's app store..) as this will give you a few sensors to play with.  If you want to use the sdk, you will need a [github](https://github.com) account


### Installing docker

Instructions for installing docker on mac can be found [here](https://docs.docker.com/docker-for-mac/install/). Instructions for installing on other operating systems can be found [here](https://docs.docker.com/engine/installation/)


### Installing git

You'll need to install git (and databox) using the mac's **Terminal** application; open Finder, click on Appilications, then Utilities and then Terminal.   This will open a new command line window. If you have any problems, watch [this](https://www.youtube.com/watch?v=zw7Nd67_aFw).  First, check to see if git is already installed, by typing:

```
git --version
```

If you get a response such as:

```
git version 2.10.1 (Apple Git-78)
```

 Then git is installed. You can move to the **installing databox** section.  Else, if the response is:

```
git: command not found
```

Then you'll need to install git.  The easiest way to install git on a mac is to use Homebrew, which you will need to install first.  Copy and paste the following, then type enter:  

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew doctor
```

You will be offered to install the Command Line Developer Tools from Apple. Confirm by clicking Install. After the installation finished, continue installing Homebrew by hitting Return again.

Now you can install git by typing:

```
brew install git
````

Check that git is now installed by running

```
git --version
```

### installing databox

Assuming you have docker and git installed, you are now ready to install databox.  Type the following into **Terminal**

```
git clone https://github.com/me-box/databox.git
```

This will create a new folder called databox.  Type

```
cd ~/databox
```

There are various ways of running databox, depending on your requirements, but we'll assume that you want to run the sdk for building apps alongside databox.  Type:

```
./databox-start sdk
```

You'll now need to wait a while whilst the scripts pull down and build the docker containers required by databox and the sdk.  Once this has finished, you should see something like:

```
[2017-10-05T14:49:52+0100 databox-start]: Databox started! Visit http://127.0.0.1:8989
databox_container-manager.1.u4k4d2kafu4f@moby    | npm info it worked if it ends with ok
databox_container-manager.1.u4k4d2kafu4f@moby    | npm info using npm@5.3.0
databox_container-manager.1.u4k4d2kafu4f@moby    | npm info using node@v8.4.0
databox_container-manager.1.u4k4d2kafu4f@moby    | npm info lifecycle container-manager@0.1.0~prestart: container-manager@0.1.0
databox_container-manager.1.u4k4d2kafu4f@moby    | npm info lifecycle container-manager@0.1.0~start: container-manager@0.1.0
databox_container-manager.1.u4k4d2kafu4f@moby    |
databox_container-manager.1.u4k4d2kafu4f@moby    | > container-manager@0.1.0 start /
databox_container-manager.1.u4k4d2kafu4f@moby    | > node src/main.js
databox_container-manager.1.u4k4d2kafu4f@moby    |
databox_container-manager.1.u4k4d2kafu4f@moby    | Using dev registry::
databox_container-manager.1.u4k4d2kafu4f@moby    | Starting UI Server!!

``` 


To check that the databox is running, open up a browser and go to [http://127.0.0.1:8989](http://127.0.0.1:8989).  You should see something like this:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/home.png" alt="dashboard home">
  <figcaption class="figure-caption text-center">databox dashboard home screen</figcaption>
</figure>

To check that the sdk is running, go to [http://127.0.0.1:8989](http://127.0.0.1:8086).  You should see:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/sdk/sdklogin.png" alt="dashboard home">
  <figcaption class="figure-caption text-center">databox dashboard home screen</figcaption>
</figure>


If you do not, go back into the terminal and type the following again:

```
./start-databox sdk
```

Now you are ready to explore the dashboard and the sdk.
