# Create a Branded Mobile Container

In this workshop we will set up a branded container. The container is the native application that Users install from the Apple AppStore and Google PlayStore. Once the User downloads the container, they will log into the app and their applications will be downloaded to their device.


**To create a branded mobile container you need**

* a Mac with Xcode installed to create iOs and Android applications
* a developer account on the Apple, Google 
* a provisioning profile for iOs
* a signing certificate for iOs
* image assets for the splash screen in multiple sizes
* image assets for the launch icon in multiple sizes

The Bodhi Builder branding tool for the Bodhi Mobile container is available on request. It should be noted that Bodhi Builder is supported on 

* Mac OS for iOs and Android development
* Windows OS for Android and Windows development

Once you have installed Bodhi Builder on your development machine, open a Terminal or Command Prompt (as Administrator on Windows), navigate to the Bodhi mobile directory and enter


````
node bodhi-builder.js
````


![](images/k2.png "container")

When Bodhi Builder starts it will run a web application on localhost:8080. (Make sure this is not blocked or there isn't andother app that is running on this port).

Click the + icon to create a new mobile container.

![](images/k3.png "container")

Enter the application name and the platform you want to deploy the container on.

![](images/k4.png "container")

Click Create.

![](images/k5.png "container")

Now you can provide the application name, version number and build. It is important to provide your own Bundle ID. This is typically based on your organisation standard package naming convention. **Do not use the default Bundle ID.**


![](images/k6.png "container")

Click Update and Next.

Select the device features you want to use. Only select what you plan to use - otherwise your app will get rejected when you submit it to the app store.


![](images/k7.png "container")

Click Update and Next.

The environment variable page is used to change the configuration of the mobile container. By default the container will load all the apps that have been provisioned for the user and will create a menu of apps for the user to choose from when they use the container. If you want to create a container that is dedicated to one application - and always launches the same application automatically without showing a menu bar - click the Edit icon and change the Menu URL option. You must then supply the application URL (shown when you publish the app to Bodhi Cloud).


![](images/k8.png "container")

Click Update and Next.

On the next screen you can change the launch icons.

![](images/k9.png "container")

Scroll to the bottom of the page and click Update icon. Click the Choose file option and locate your icon images.

Click Update and Next.

![](images/k10.png "container")


On the next screen you can change the launch image. This is the splash screen that is shown when the application first starts.

![](images/k11.png "container")

Scroll to the bottom of the page and click Update Launch image. Click the Choose file option and locate your Launch images.

![](images/k12.png "container")

On the next screen you can change the styling of the container. This includes the text and container colours. These are CSS properties. 

![](images/k13.png "container")

Click Update and Next.


On the next screen you can change the styling of the navigation bar. This includes the text colour, background colour and the logo image. 


![](images/k16.png "container")

Click Update and Next.

On the next screen you must provide your Apple Developer certificate and mobile provisioning file. Click Choose File to locate the files. 

![](images/k15.png "container")

Click Save to save the location once you have selected the file. 

Click Next.


![](images/k17.png "container")

Now you are ready to create your own cusom mobile container. There are several options to try - for example you can publish the application to HockeyApp (if you have an account). In this exercise we will just launch the app in Xcode. 

Click Open in Xcode.

![](images/k18.png "container")

Once Xcode has launched and loaded your custom Bodhi mobile container, connect your iPhone, iPad or iPod Touch. This will allow you to publish your app to your mobile device. 

> You must register your device with your mobile provisoning file so that you are allowed to publish apps to your device. 

![](images/k20.png "container")

When the project build has completed, you are ready to run the app on your device.

![](images/k21.png "container")

If you don't want to run the app on your device, you can always use the iOs simulator.

![](images/k22.png "container")

To run the app on your device or the simulator - press the Play icon in Xcode. This will publish and launch the app on your device.

![](images/k23.png "container")

You will see your app icon written to your device and then your application splash screen will apear. Cool eh?

![](images/k24.png "container")

The Bodhi Mobile login page is displayed. (This is also customisable and should be available by Q3 2015). Log into the app with your credentials.

![](images/k25.png "container")

Your apps are now available in your own custom container.

![](images/k26.png "container")

You can now use Xcode to create your production build and submit your app to the appstore.



For errors or feedback with any of these labs please contact support@hotschedules.com






