# Provision and deploy an App


In this second workshop, we will deploy the Reveal application. The Reveal app makes use of server side jobs to process inbound data into aggregated data in real time. The app is installed from the Google Play or Apple AppStore.


## Adding the Reveal jobs

We need to add the Reveal jobs to process inbound data for our stores.

All applications, whether mobile, agent or server side jobs, are added to your account using the Bodhi Shop tool. 

From your desktop browser, log into Bodhi Tools at https://tools.bodhi.space/. 

Scroll down to Bodhi Shop and click to launch.

![](images/40.png "shop0")

In Bodhi Store, click **My Job Apps**. This should display the job apps you have installed in your environment. Just as with the mobile and agent apps pages, there should not be any job apps deployed in your environment if this is the first time you have clicked through to the Job apps page.

![](images/b1.png "job")

To add a Job, click on Job Apps link.

![](images/b2.png "job")

The public Bodhi Job Engine Apps Shop is displayed. Scroll through the list of Jobs.

![](images/b3.png "job")

Look for the **Reveal Aggregation (day)** job and click Install to install and schedule the Job. The Reveal Aggergation job (day) creates daily KPI's for each store. 

![](images/b4.png "job")

A dialog is displayed. The Job needs to be configured. For the job name enter **day**

![](images/b5.png "job")

You can select a specific store to run the job for - or you can leave the store property blank to run the job for all stores.

![](images/b6.png "job")

You can schedule a frequency to run the job. For now - just leave the default at 10 minutes. Click continue.

![](images/b7.png "job")

The Reveal Aggregation (day) Job should now be added to your jobs in your namespace and scheduled to run every 10 minutes.

![](images/b8.png "job")

Click the Categories drop down and click **Job Engine Apps**

![](images/b9.png "job")

Look for the **Reveal Aggregation (hour)** job and click Install to install and schedule the Job. The Reveal Aggergation job (hour) creates hourly KPI's for each store. These consist of 15-minute interval aggregations.

![](images/b10.png "job")

A dialog is displayed. The Job needs to be configured. For the job name enter **hour**

![](images/b11.png "job")

As we want to run the job for all stores, leave the store selection blank. Press Continue.

![](images/b12.png "job")

The Reveal Aggregation (hour) Job should now be added to your jobs in your namespace and scheduled to run every 10 minutes.

![](images/b13.png "job")



## Add the Reveal app

All applications, whether mobile, agent or server side jobs, are added to your account using the Bodhi Shop tool. 

From your desktop browser, log into Bodhi Tools at https://tools.bodhi.space/. 

Scroll down to Bodhi Shop and click to launch.

![](images/40.png "shop0")


Click the 'Mobile Apps' link or Categories-> Mobile Apps to navigate to the Global (public) Bodhi Shop.

![](images/c1.png "shop2")

In the public Bodhi shop you can see the mobile applications that are available for installation into your account. 



![](images/c2.png "shop3")

If you want to review an app before installing it, just click on the app logo to view the app details. 

If you want to add an application to your account just click the Install button. When the app has been added to your account, you will be take to the detail page for that application. 

![](images/c3.png "shop4")

Look for the **HotSchedules Reveal** app in the Standalone Apps section and then click the Install button to add the application to your namespace. 


![](images/c4.png "shop4")

A popup will inform you that new data structures will be added to your namespace. Click Continue.

![](images/c5.png "shop4")

The new data structures will be added along with the Reveal application.

![](images/c6.png "shop5")

Now you can see that the Reveal app has been installed in your namespace. By default, all apps are added with one user assigned - this is the user who installed the app into the namespace, usually the admin user on the account. 

![](images/c7.png "shop5")

To add more users to the account click the **Add User** drop down and select the users that require access to this application. For the Reveal app, this will be anyone who needs to see the real time KPI's for the stores.


 
 
## Installing HotSchedules Reveal

Now we will install HotSchedules Reveal from the app store. Reveal is a Standalone application, which means it runs in its own container. The Reveal web app will be lauched immediately when the user launches the app on their phone. The user will not have to pick from a selection of apps as you saw in the Bodhi Mobile app. 

From your iPhone launch Apple Store or from your Android Phone launch Google Play.  
Search for **HotSchedules Reveal**. Reveal is an app that displays real time KP's from your store.

Once you have found HotSchedules Reveal, install the app.

<img src="images/b14.png" alt="Drawing" style="width: 480px;"/>
 
 
Launch the application and log in with your credentials. 



<img src="images/r8.png" alt="Drawing" style="width: 320px;"/>

On first log in, the app will be downloaded from Bodhi Cloud. The first log in will take more time that subsquent log ins as a result.


<img src="images/r9.png" alt="Drawing" style="width: 320px;"/>

Once the app loads into the HotSchedule Reveal mobile device, you will see the Favorites screen. it will be blank at first but we can add some KPI's to in in a minute.

<img src="images/r10.png" alt="Drawing" style="width: 320px;"/>

Tap on the upper left menu bar and select 'Sales dashboard'. 

At the top of the screen you can see the Dashboard name, then the Store name with the current weather conditions for the store. Under the Store name there is a status bar that displays the date and when the last update was made. This is also a Date picker - so if you tap the date you can use the Date Picker to change the timeframe you are looking at.

Each dashboard consists of tiles with the KPI name, value and variance in % and amount from a year ago. 

<img src="images/r13.png" alt="Drawing" style="width: 320px;"/>

If you tap any tile you will drill down into the detail for that KPI.

On this screen you see the Active (current), the Historical (one year today) and Previous (this time last week) metrics. You can tap each icon to switch these off and remove the series from the chart.



<img src="images/r11.png" alt="Drawing" style="width: 320px;"/>

Tapping the Period at the bottom of the screen will change the display from Day Part (P) to Day (D), Week (W) and Month (M).


<img src="images/r14.png" alt="Drawing" style="width: 320px;"/>

If you scroll up, you will see a break down of the KPI by increments throughout the day, week or month. For example if you are looking at the Day View, you will see sales by 15-minute intervals. 



> Bodhi captures all of the raw transactions from the POS in real time but shows you an aggregated view of the data in the Reveal app

<img src="images/r15.png" alt="Drawing" style="width: 320px;"/>


If you double tap the chart, it will embed the chart into the default email client of your mobile device and you can send that to a team member or manager for review.


<img src="images/r20.png" alt="Drawing" style="width: 320px;"/>

Once you have sent your email, click the back arrow in the title bar of the application. Looking at the Sales dashboard you can pivot the view to look at all the stores compared against themselves.


<img src="images/r12.png" alt="Drawing" style="width: 320px;"/>



 