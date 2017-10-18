---
layout: base
title:  a first look at the dashboard
---

The databox dashboard is the interface that you use to install apps and drivers.  A quick recap: a driver is software that communicates with datasources, and apps are **databox** applications that process your personal data on the box.  This section assumes that you have installed databox on a machine; if you have not, please go through [these instructions](/gettingstarted/install).  

Although you do not have to install the databox dashboard on your phone, we'd recommend it as it'll give you access to some of your phone's sensors, which will expand the number of apps that you can run.  Before you get started, you'll need the IP address of the computer that you are running your databox on.  If you do not know it, the simplest way is to use an online service such as <a href="https://www.whatismybrowser.com/detect/what-is-my-local-ip-address" target="_blank">what is my browser</a>

### installing on a phone 

First, **ensure that you are on the same network as the machine that is running databox.**

To install the app on a phone, go to the Google Play store or Apple App store and look for the databox app <img src="/images/gettingstarted/databoxicon.png" style="display:inline-block; width: 30px">.  Once started, if the app does not automatically discover your databox, give it the IP address of the databox machine.

### running in a web browser

To run in a web browser, if you are on the same machine as your databox, go to <a href="http://127.0.0.1:8989" target="_blank">http://127.0.0.1:8989</a> (opens in new tab).  Else, enter the IP address of the machine running databox, i.e. http://[databoxipaddress]:8989

### the dashboard interface.

When you first load up, teh app will attempt to find your databix.  If it fails, you will be prompted to enter the databox address:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/connectionerror.png" width="30%" alt="dashboard connection error">
  <figcaption class="figure-caption text-center">dashboard connection error</figcaption>
</figure>

Type in the address that the databox is running on.  Once successful you should see the following screen:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/homescreen.png" width="30%" alt="dashboard home screen">
  <figcaption class="figure-caption text-center">dashboard home screen</figcaption>
</figure>

On the top right hand of the screen is the menu.  Click on it and you should see the following:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/menu.png" width="30%" alt="dashboard menu">
  <figcaption class="figure-caption text-center">dashboard menu</figcaption>
</figure>

### running apps, drivers and stores

"Out of the box" the databox has no apps or drivers running on it.  If you click on Apps or Drivers you'll simply see an empty list for each as follows:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/runningempty.png" alt="running apps">
  <figcaption class="figure-caption text-center">running apps,drivers,stores</figcaption>
</figure>


You should rarely need to click on the "Stores" menu item, as stores are automatically loaded up as required when a new driver/app is installed.

### the app store

The default app store has several simple sample apps, which you can use to 'smoke test' the databox.   Click on "App Store" to take a look:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/appstore.png" width="30%" alt="app store">
  <figcaption class="figure-caption text-center">app store</figcaption>
</figure>

If you have already published an app (by following [the sdk walkthrough](/gettingstarted/sdk)) then you should see it in the list here.  The simplest possible app is **os monitor**.  Before we install it, we need to install the **osmonitor** driver, by going to the **Driver Store**:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/driverstore.png" width="30%" alt="driver store">
  <figcaption class="figure-caption text-center">driver store</figcaption>
</figure>

Click on **osmonitor** and follow the install instructions.  Once installed, after a short wait you should see it listed on the Drivers page.  Now you are ready to install the os monitor app.  Go back to Apps, and click on os monitor.   

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/osmonitorrunninglist.png" width="30%" alt="driver store">
  <figcaption class="figure-caption text-center">driver store, osmonitor</figcaption>
</figure>

Now you are ready to install the app.  Go to the App Store and select **os monitor**.  You'll be presented with an install dialogue:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/osmonitorinstall.png" width="30%" alt="app store, install osmonitor">
  <figcaption class="figure-caption text-center">app store, install osmonitor</figcaption>
</figure>

The osmonitor app requires access to all of the osmonitor's datasources (each of the 1,5 and 15 minute load averages are a datasource, as is the total freememory): 

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/osmonitorselectdatasources.png" width="30%" alt="app store, select datasources">
  <figcaption class="figure-caption text-center">app store, select datasources</figcaption>
</figure>

You will be prompted to agree to give access to all of them, and once done you should have:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/osmonitorselecteddatasources.png" width="30%" alt="app store, selected datasources">
  <figcaption class="figure-caption text-center">app store, selected datasources</figcaption>
</figure>

Now click on INSTALL, and after a short delay, you should see osmonitor it listed in the running apps:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/osmonitorrunningapplist.png" width="30%" alt="driver store">
  <figcaption class="figure-caption text-center">driver store, osmonitor</figcaption>
</figure>

Click on it and you should see a several plots, which are reading live os system data from the databox:


<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/osmonitoroutput.png" width="30%" alt="osmonitor output">
  <figcaption class="figure-caption text-center">osmonitor output</figcaption>
</figure>


### installing sensingkit

To get access to a few more sensors, and apps that make use of them, you can enable access to your phone's sensors by installing the sensingkit driver.  Go to the Driver Store page and select sensingkit.  Follow the install instructions:

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/installsensingkit.png" width="30%" alt="install sensingkit driver">
  <figcaption class="figure-caption text-center">install sensingkit driver</figcaption>
</figure>

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/sensingkitrunning.png" width="30%" alt="sensingkit running">
  <figcaption class="figure-caption text-center">sensingkit running</figcaption>
</figure>

Once you see sensingkit is running, you can enable various sensors.  Go back to the menu and click on "Mobile Sensor Data". 

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/installmobile.png" width="30%" alt="sensingkit running">
  <figcaption class="figure-caption text-center">sensingkit - install mobile sensors</figcaption>
</figure>

 Click on "Enable Mobile Sensor Data" and this should open up a list of sensors supported by the phone.

<figure class="figure">
  <img class="thumbnail" src="/images/gettingstarted/dashboard/sensingkitchosensensors.png" width="30%" alt="sensingkit sensors">
  <figcaption class="figure-caption text-center">enabled sensingkit sensors</figcaption>
</figure>

Select light and accelerometer. Now you can go back to the App Store and test an app that makes use of these sensors.  Try installing and running the **light graph** app.  Once installed, if you click on it, it should bring up a graph showing the current light reading in lux (from your phone's camera).