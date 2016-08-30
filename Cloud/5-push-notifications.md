# Push Notifications

In this workshop we will look at setting up Push Notifications. 


##Prerequisites

**To receive Push Notifications you need** 

* Bodhi Mobile installed on your ios or android device
* Accepted Push Notifications for your device
* A valid user account that can access the API

You need a version of the Bodhi Mobile native application(s) which supports registration as a push notification client.  

When you log into the mobile client, the client will pop up an alert and ask you if you want to accept push notifications. If the user accepts, the mobile client will create a registration token and store this using the BodhiDevice type. 

The device challenge and authorisation is a common practice and adheres to Apple and Google's guidelines for user authorised push notifications.


## Check the device is registered 

Before starting to build your push notification application, validate the target device is registered for notifications.

To validate the device is registered, query the BodhiDevice type

````
curl https://<server addr>/<namespace>/resources/BodhiDevice 
````



## Sending a Push notification

Once one or more devices have been registered you can send notifications via the API Server’s “notifications” endpoint.  

The URI for this is:

````
	https://<server addr>/<namespace>/notifications
````

The notification expects a POST request where the body is a JSON document of the following form:

````
	{
	 “to”: {
		 [“type”: “BodhiUser“ | “BodhiDevice”]?,
		  “where”: <query document>
         },
	 “payload”: <payload document>
	}
````

You can send a notification to a specific target type:

* a user
* a device type

The “type” property of the “to” document determines the target type for the query supplied by the “where” property.  
The “type” is optional and may contain either BodhiUser or BodhiDevice. BodhiDevice is the default if this property is missing. 


The “payload” document can contain any legal JSON document.  However, if you want to display a text alert on the target device then the payload must include the “message” property in the JSON of the payload document

````
{
 "payload": {"message":"this is my real message"}
}
````

## Example using CURL

In this example we will send a notification to all Android users using CURL. You need to have a valid user account to access the API. 

1. Create a text file and paste the following contents. In this example the text file is called 'message.json' - but you can call it anything you want.
 

````
{
 "to": {"type": "BodhiUser", "where": {"username": "YOURUSERNAME"}},
 "payload": {"message":"Please join us for cocktails and canapes at 4"}
}
````
Note: Collapse the JSON into one line to mitigate the possibility of errors through hidden characters.

2. Using CURL send a PUSH request sending the message file. 
In this example our namespace is called 'tiffles'.
 

````
curl -X POST -H "Content-Type: application/json" -u USERNAME:PASSWORD 
https://api.bodhi.space/tiffles/notifications -d @message.json
````



For errors or feedback with any of these labs please contact support@hotschedules.com






