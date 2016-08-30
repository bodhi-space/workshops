# The HotSchedules Application API

The HotSchedules IoT Platform provides a new way to interact with HotSchedules Application Data through a REST API.  

[Application Services](https://github.com/bodhi-space/workshops/blob/master/Application/hs_api.md#application-services)   
[Specification](https://github.com/bodhi-space/workshops/blob/master/Application/hs_api.md#specification)   
[Using Java](https://github.com/bodhi-space/workshops/blob/master/Application/hs_using_java.md)   

Customers and developers have a choice when integrating with the HotSchedules Labor application. Data moves between the HotSchedules IoT platform and the HotSchedules application. You may choose to use the Platform API to get / post data but you must ensure the platform server side processes are running to ensure that data flows to the HotSchedules Application.

To understand the API, read the API [Specification](https://github.com/bodhi-space/workshops/blob/master/Application/hs_api.md#specification)

## Application Services

[Employee](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md)  
[Labour](https://github.com/bodhi-space/workshops/blob/master/Application/hs_labour.md)  
[Organisation](https://github.com/bodhi-space/workshops/blob/master/Application/hs_org.md)  
[Sales](https://github.com/bodhi-space/workshops/blob/master/Application/hs_sales.md)  
[Schedule](https://github.com/bodhi-space/workshops/blob/master/Application/hs_schedule.md)  
[Timecard](https://github.com/bodhi-space/workshops/blob/master/Application/hs_timecard.md)  
[Transactions](https://github.com/bodhi-space/workshops/blob/master/Application/hs_transactions.md)  



## Specification



The Application API is defined as follows


````
<Host><Namespace><Platform Resource><Concept Id><Store Id><Method>?<Params>
````

Property | Definition | Actual value or example
------------ | ------------- | ------------
Host | The Production instance  | <https://api.bodhi.space>
Namespace | The Namespace is your account name | e.g. TifflesCakes | 
Platform Resource |  The Application API makes use of [Vert.x](http://vertx.io/) to integrate with Hotschedules Labor. The platform resource is accessed using as "controllers/vertx/". The application is "hotschedules" |   controllers/vertx/hotschedules
Concept Id | The ID of the concept or brand | e.g. 1
Store Id | The ID of the store | e.g. 2
Method | The resource method we are calling | e.g. getEmpInfo
Params | Additional information to pass to the operation | e.g. active_employee=true

 

## Example

Tiffles is a two concept chain of coffee shops (concept 1) and bake shops (concept 2). We want to get information about all the active employees for our Palo Alto coffee store, Store number 2. 

The URL request would be constructed as follows:  

Property | Value 
------------ | -------------  
Host | api.bodhi.space 
Namespace |  tiffles  
Resource | controllers/vertx/hotschedules  
Concept |  1 
Store | 2  
Method | getEmpInfo  
Params | active_only=true  

The URL looks like this:

````
https://api.bodhi.space/tiffles/controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true
````

Calling this through CURL:

````
curl -X GET -H "Content-Type:application/json" -u username:password 
"https://api.bodhi.space/tiffles/controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true"
````



**Technical Note**
If you are using the HS IoT Platform API and the HS Application API you should be aware of the subtle differences between the two API definitions. The HS Platform API is a RESTful API built  on the HS Platform data model. It follows the standard convention for API calls - using HTTP VERBS to operate with data objects or services exposed on the platform.

The HS Application API is a RESTful facade built on the orginal HotSchedules WS* SOAP API and preserves the same API call without the complexity of adding all the SOAP boiler plate code. It is for this reason that the Service methods include the operating verb (keywords such as 'get' and 'set') when it is by strict definition, not required.


