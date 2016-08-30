# HotSchedules Labor Integration

This documentation is intended for developers looking to integrate to the HS IoT Platform with the purpose of building a bi-directional integration into their point of sale systems. 

While the HS IoT Platform exposes many API's and can be accessed through several means, this documentation focuses on two specific use cases using the Platform API

1. integration to the general or canonical data types
2. integration to the data types required by HotSchedules Labor

If you only want to integrate to the HotSchedules Labor product then you only need to use the data types for HotSchedules Labor. If you want to use the platform for other purposes or applications then you need to use the canonical data structures.  
If you want to use the platform and labor - then you need to write to both data structures.


- [Prerequisites](#prereq)
- [The API in 2 minutes](#api)
- [GET and POST data](#get)
- [HS Labor Data](#labour) 
- [Canonical Data](#canonical)



## <a name="prereq">Prerequisites</a>

To access the Platform API and execute the queries you will need the following:

1. A Platform account 
2. Code or shell script that can make REST requests to the Platform API.


## <a name="api">The API in 2 minutes</a>


The Platform API consists of four parts

- host
- namespace
- resource
- query

The **host** is the public URL of the Platform Cloud. This is always <https://api.bodhi.space/>. Note all requests are made over **HTTPS**

The **namespace** is the name of your Platform account or “tenant”. In this document we will assume our namespace is called “organics” - an account that exists for the organic chain of cafes located in the San Francisco Bay Area.

The **resource** is the name of the data structure (or “type”) that you want to access.  An example or a resource is SalesItem or SalesTransaction. The resource is always prefixed with the '**resources/**' keyword.

The **query** is the typical type of query that you would make in the browser. It can be a simple request to get all results or a limited set of results using a where clause - or can be more complex and provide aggregated results. 

The **results** returned from a query, known as documents - and are returned in JSON notation.

A request is constructed like this

````
<host>/<namespace>/resources/<resource>/query
````

Example 1: A query on the Organics account with no query:

````
https://api.bodhi.space/organics/resources/Store
````

Example 2: A query on the Organics account with a query:

````
https://api.bodhi.space/organics/resources/Store?where={'display_name': { $eq: 'Carrots' }}
````


API documentation for all Platform types - including any that you have created yourself, can be located at <https://api.Platform.space/apidocs/index.html>


## <a name="get">GET and POST data</a>

To get familiar with the API, first log into **https://tools.bodhi.space/query/**. This will ensure that any REST queries you make via the browser will be authenticated and correctly formatted.

![login](../images/10.png "login")

#### GET Data

In the Bodhi Query tool, enter the name of the data type you want to access in the first input field. In this case you want to fetch all stores from the data type called 'Store' - so enter **Store** in the input box.

![querytool](../images/labour1.png "get")

Before you press Send to execute the query, look at the middle of the page. You can see that the Query tool has built up the query you are about to send to the Platform API. It should look something like this:

````
https://api.bodhi.space/organics/resources/Store
````

Press Send to Execute the query. If you have any stores populated in your account you should see some data.


Now lets test the same query in a browser tab. Press the clipboard icon in the middle of the page to copy the query to your clipboard. 

Open a new browser tab. Paste the query from the clipboard buffer into the address bar. Hit return to execute the query. you should see the same results in your browser window. You now know how to make and structure the REST requests against the platform API.


#### POST Data

To post data to the platform API go back to the Platform Query tool. Click the drop down option (marked GET) to change the operation to POST. 

![querytoolpost](../images/labour2.png "post")

The query tool will create a pre-populated JSON structure for you, so you can write to the data type. Go ahead and populate the data structure. Note: you don't have to populate all the properties - but some are mandatory. If you just want to save time, the following example is a bare minimum that you can POST.  You can copy the content and post this instead.


````
{
	"name": "Carrots",
	"display_name": "Carrots",
	"store_number": "4902201",
	"organization_name": "Organics",
	"currency": "USD"
}
````

![querytoolpostdata](../images/labour3.png "postdata")

When you are ready, press Send to post the data to the platform API. The Platform should respond with a 204 saying the data was created. If you made any syntax errors you will be informed and the post will fail.



#### Dictionary of types

Before looking at the data types you need to populate or plan to query from the platform, you should take a look at the dictionary of data types located here **https://api.bodhi.space/apidocs/index.html**

Note: if you want to access the documentation without having to log in again, you can do so by keeping the Query tool open in one tab (your authenticated session open) and opening a new tabe and entering the following URL in the browser on one line:

````
https://api.bodhi.space/apidocs/index.html?url=
https://api.bodhi.space/organics/api-docs#!/Store
````

This will open the browser and take you to the Store data definition as shown in the diagram below.


![swagger](../images/labour4.png "swagger")


You can interact with the API in the same way that you tested the API using the query tool.

**NOTE:** It is recommended that you use the API docs to test and validate the API definition because the API docs are a live specification of the current API. This document, while providing some schema information, may become out of date over time as the API definition changes.


## <a name="labour">HS Labor Data</a>

To push data to HotSchedules Labor scheduling software only, the following data types need to be populated:

Seed data (changes infrequently) 
- HSStoreEmployee   
- HSStoreEmployeeJob     
- HSRevenueCenter 
- HSSalesCategory 
- HSSalesCategoryRollup 
- HSStoreJob  

Transactional data (changes on a per day basis)
* HSSalesTransaction 
* HSSchedule 
* HSTimecard 





### HSStoreEmployee


````
HSStoreEmployee {
			hr_id (string, optional),
			name (PersonName),
			employment_period (DatePeriod, optional),
			store_id (string, optional),
			store (InStoreReference),
			birthdate (date-time, optional),
			status (string, optional),
			phone_numbers (string, optional),
			instore_id (string),
			emails (string, optional),
			addresses (Array[PostalAddress], optional),
			nickname (string, optional)
}
````

**HSEmployee Embedded type definition**


````
PersonName {
			family_name (string),
			honorific_prefix (string, optional),
			honorific_suffix (string, optional),
			middle_name (string, optional),
			formatted_name (string, optional),
			given_name (string, optional)
}
KeyValuePair {
			key (string),
			value (string, optional)
}
EmployeePosition {
			employee_id (string, optional),
			employee_reference (InStoreReference),
			employment_period (DatePeriod, optional),
			store_reference (InStoreReference),
			job_reference (InStoreReference),
			regular_rate (BodhiCurrency, optional),
			overtime_rate (BodhiCurrency, optional),
			store_id (string, optional),
			job_id (string, optional),
			status (string, optional),
			doubletime_rate (BodhiCurrency, optional)
}
InStoreReference {
			id (string),
			name (string, optional)
}
DatePeriod {
			from (date-time),
			to (date-time, optional)
}
BodhiCurrency {
			code (object) = [''],
			value (integer),
			scale (integer, optional)
}
PostalAddress {
			country (object, optional) = [''],
			extended_address (string, optional),
			postal_code (string, optional),
			region (string, optional),
			street_address (string, optional),
			type (string, optional),
			locality (string, optional)
}
````


### HSStoreEmployeeJob   


````
HSStoreEmployeeJob {
	employee_id (string, optional),
	regular_rate (BodhiCurrency, optional),
	overtime_rate (BodhiCurrency, optional),
	external_ids (Array[KeyValuePair], optional),
	store_id (string, optional),
	employee (InStoreReference),
	job (InStoreReference),
	store (InStoreReference),
	job_id (string, optional),
	doubletime_rate (BodhiCurrency, optional)
}
````

**HSEmployeePosition Embedded type definition**


````
InStoreReference {
			id (string),
			name (string, optional)
}
DatePeriod {
			from (date-time),
			to (date-time, optional)
}
BodhiCurrency {
			code (object) = [''],
			value (integer),
			scale (integer, optional)
}
````





 
### HSRevenueCenter 

````
HSRevenueCenter {
			store_id (string),
			instore_name (string, optional),
			display_name (string, optional),
			instore_id (string, optional)
}
````



### HSSalesCategory 

````
HSSalesCategory {
			store_id (string),
			instore_name (string, optional),
			display_name (string, optional),
			instore_id (string, optional)
}
````


### HSSalesCategoryRollup 


````
HSSalesCategoryRollup {
			tax_id (string, optional),
			tax_exempt (boolean, optional),
			quantity (Real),
			order_id (string, optional),
			timestamp (date-time),
			order_number (integer, optional),
			canceled_closed (boolean, optional),
			description (string, optional),
			external_ids (Array[KeyValuePair], optional),
			store_id (string),
			discount_total (BodhiCurrency, optional),
			voided_closed (boolean, optional),
			tax_total (BodhiCurrency, optional),
			non_sales_item (boolean, optional),
			gross_total (BodhiCurrency, optional),
			sales_category (InStoreReference, optional),
			modified (boolean, optional),
			tax_index (integer, optional),
			department (InStoreReference, optional),
			unit_price (BodhiCurrency, optional),
			business_day (string, optional),
			transaction_id (string),
			net_total (BodhiCurrency),
			carry_out (boolean, optional),
			currency_scale (integer, optional),
			tax_details (Array[SalesAmount], optional),
			type (InStoreReference, optional),
			currency_code (object, optional) = [''],
			discount_details (Array[SalesAmount], optional),
			discounted (boolean, optional)
}
````


**HSSalesCategoryRollup Embedded type definition**


````
KeyValuePair {
			key (string),
			value (string, optional)
}
BodhiCurrency {
			code (object) = [''],
			value (integer),
			scale (integer, optional)
}
InStoreReference {
			id (string),
			name (string, optional)
}
SalesAmount {
			rate (Real, optional),
			amount (BodhiCurrency, optional),
			id (string, optional),
			category (string, optional),
			index (integer, optional)
}
````




### HSStoreJob  

````
HSStoreJob {
		regular_rate (BodhiCurrency, optional),
		overtime_rate (BodhiCurrency, optional),
		store_id (string),
		instore_name (string),
		instore_id (string),
		doubletime_rate (BodhiCurrency, optional)
}
````


**HSStoreJob Embedded type definition**

````
BodhiCurrency {
		code (object) = [''],
		value (integer),
		scale (integer, optional)
}
````


### HSSalesTransaction 

````
HSSalesTransaction {
		tax_id (string, optional),
		gratuity_total (BodhiCurrency, optional),
		tax_exempt (boolean, optional),
		order_id (string, optional),
		timestamp (date-time),
		order_number (integer, optional),
		canceled_closed (boolean, optional),
		item_count (integer, optional),
		external_ids (Array[KeyValuePair], optional),
		store_id (string),
		discount_total (BodhiCurrency, optional),
		voided_closed (boolean, optional),
		tax_total (BodhiCurrency, optional),
		employee (InStoreReference, optional),
		change_total (BodhiCurrency, optional),
		gross_total (BodhiCurrency, optional),
		excess_tender (boolean, optional),
		auto_tendered (boolean, optional),
		point_of_sale_brand (string, optional),
		training (boolean, optional),
		point_of_sale (InStoreReference, optional),
		tender_details (Array[SalesAmount], optional),
		modified (boolean, optional),
		tax_index (integer, optional),
		department (InStoreReference, optional),
		business_day (string, optional),
		order_opened_at (date-time, optional),
		net_total (BodhiCurrency, optional),
		carry_out (boolean, optional),
		revenue_center (InStoreReference, optional),
		tender_total (BodhiCurrency),
		change_details (Array[SalesAmount], optional),
		customer (InStoreReference, optional),
		guest_count (Real, optional),
		car_count (Real, optional),
		currency_scale (integer, optional),
		tax_details (Array[SalesAmount], optional),
		type (InStoreReference, optional),
		currency_code (object, optional) = [''],
		discount_details (Array[SalesAmount], optional),
		discounted (boolean, optional),
		table (InStoreReference, optional),
		order_closed_at (date-time, optional)
}
````

**HSSalesTransaction Embedded type definition**


````
BodhiCurrency {
		code (object) = [''],
		value (integer),
		scale (integer, optional)
}
KeyValuePair {
		key (string),
		value (string, optional)
}
InStoreReference {
		id (string),
		name (string, optional)
}
SalesAmount {
		rate (Real, optional),
		amount (BodhiCurrency, optional),
		id (string, optional),
		category (string, optional),
		index (integer, optional)
}
````


### HSSchedule 

````
HSStoreSchedule {
		store_id (string),
		employee (InStoreReference),
		job (InStoreReference),
		start_at (date-time),
		external (InStoreReference),
		stop_at (date-time)
}
````


**HSSchedule Embedded type definition**

````
InStoreReference {
		id (string),
		name (string, optional)
}
````


### HSTimecard 


````
HSTimecard {
		employee_id (string, optional),
		employee_reference (InStoreReference, optional),
		store_reference (InStoreReference, optional),
		job_reference (InStoreReference, optional),
		regular_rate (BodhiCurrency, optional),
		overtime_rate (BodhiCurrency, optional),
		external_ids (Array[KeyValuePair], optional),
		store_id (string),
		ended_at (date-time),
		job_id (string, optional),
		started_at (date-time),
		business_day (string, optional),
		doubletime_rate (BodhiCurrency, optional)
}
````

**HSTimecard Embedded type definition**

````
InStoreReference {
		id (string),
		name (string, optional)
}
BodhiCurrency {
		code (object) = [''],
		value (integer),
		scale (integer, optional)
}
KeyValuePair {
		key (string),
		value (string, optional)
}
````




## <a name="canonical">Canonical Data</a>

To push data to HotSchedules IoT Platform, the following data types can be populated. Note the data is accessible to any application deployed on the platform (assuming it has been granted permission). 

Seed data (changes infrequently) 
- Employee   
- EmployeePosition    
- RevenueCenter 
- SalesCategory 
- StoreJob  

Transactional data (changes on a per day basis)
* SalesTransaction 
* Schedule 
* Timecard 
 
 
 
 
## Employee


````
Employee {
			name (PersonName),
			external_ids (Array[KeyValuePair], optional),
			birthdate (date-time, optional),
			status (string, optional),
			phone_numbers (string, optional),
			emails (string, optional),
			addresses (Array[PostalAddress], optional),
			nickname (string, optional)
}
````

**Employee Embedded type definition**


````
PersonName {
			family_name (string),
			honorific_prefix (string, optional),
			honorific_suffix (string, optional),
			middle_name (string, optional),
			formatted_name (string, optional),
			given_name (string, optional)
}
KeyValuePair {
			key (string),
			value (string, optional)
}
PostalAddress {
			country (object, optional) = [''],
			extended_address (string, optional),
			postal_code (string, optional),
			region (string, optional),
			street_address (string, optional),
			type (string, optional),
			locality (string, optional)
}
````




### EmployeePosition

````
EmployeePosition {
			employee_id (string, optional),
			employee_reference (InStoreReference),
			employment_period (DatePeriod, optional),
			store_reference (InStoreReference),
			job_reference (InStoreReference),
			regular_rate (BodhiCurrency, optional),
			overtime_rate (BodhiCurrency, optional),
			store_id (string, optional),
			job_id (string, optional),
			status (string, optional),
			doubletime_rate (BodhiCurrency, optional)
}
````

**EmployeePosition Embedded type definition**

````
InStoreReference {
			id (string),
			name (string, optional)
}
DatePeriod {
			from (date-time),
			to (date-time, optional)
}
BodhiCurrency {
			code (object) = [''],
			value (integer),
			scale (integer, optional)
}
````


###  RevenueCenter

````
RevenueCenter {
			store_id (string),
			instore_name (string, optional),
			display_name (string, optional),
			instore_id (string, optional)
}
````




### SalesCategory 

````
SalesCategory {
			store_id (string),
			instore_name (string, optional),
			display_name (string, optional),
			instore_id (string, optional)
}
````


### StoreJob  


````
StoreJob {
			regular_rate (BodhiCurrency, optional),
			overtime_rate (BodhiCurrency, optional),
			store_id (string),
			instore_name (string),
			instore_id (string),
			doubletime_rate (BodhiCurrency, optional)
}
````

**StoreJob Embedded type definition**


````
BodhiCurrency {
			code (object) = [''],
			value (integer),
			scale (integer, optional)
}
````



### SalesTransaction 
````
SalesTransaction {
			tax_id (string, optional),
			gratuity_total (BodhiCurrency, optional),
			tax_exempt (boolean, optional),
			order_id (string, optional),
			timestamp (date-time),
			order_number (integer, optional),
			canceled_closed (boolean, optional),
			item_count (integer, optional),
			external_ids (Array[KeyValuePair], optional),
			store_id (string),
			discount_total (BodhiCurrency, optional),
			voided_closed (boolean, optional),
			tax_total (BodhiCurrency, optional),
			employee (InStoreReference, optional),
			change_total (BodhiCurrency, optional),
			gross_total (BodhiCurrency, optional),
			excess_tender (boolean, optional),
			auto_tendered (boolean, optional),
			point_of_sale_brand (string, optional),
			training (boolean, optional),
			point_of_sale (InStoreReference, optional),
			tender_details (Array[SalesAmount], optional),
			modified (boolean, optional),
			tax_index (integer, optional),
			department (InStoreReference, optional),
			business_day (string, optional),
			transaction_id (string),
			order_opened_at (date-time, optional),
			net_total (BodhiCurrency, optional),
			revenue_center (InStoreReference, optional),
			tender_total (BodhiCurrency),
			change_details (Array[SalesAmount], optional),
			customer (InStoreReference, optional),
			guest_count (Real, optional),
			service_type (string, optional),
			delivery_type (string, optional),
			car_count (Real, optional),
			currency_scale (integer, optional),
			tax_details (Array[SalesAmount], optional),
			type (InStoreReference, optional),
			currency_code (object, optional) = [''],
			discount_details (Array[SalesAmount], optional),
			discounted (boolean, optional),
			table (InStoreReference, optional),
			order_closed_at (date-time, optional)
}
````

**SalesTransaction Embedded type definition**


````
BodhiCurrency {
		code (object) = [''],
		value (integer),
		scale (integer, optional)
}
KeyValuePair {
		key (string),
		value (string, optional)
}
InStoreReference {
		id (string),
		name (string, optional)
}
SalesAmount {
		rate (Real, optional),
		amount (BodhiCurrency, optional),
		id (string, optional),
		category (string, optional),
		index (integer, optional)
}
````

### Schedule 
````
StoreSchedule {
		store_id (string),
		employee (InStoreReference),
		job (InStoreReference),
		start_at (date-time),
		external (InStoreReference),
		stop_at (date-time)
}
````

**StoreSchedule Embedded type definition**


````
InStoreReference {
		id (string),
		name (string, optional)
}
````


### Timecard 

````
Timecard {
		breaks (Array[TimecardBreak], optional),
		employee_id (string, optional),
		employee_reference (InStoreReference, optional),
		store_reference (InStoreReference, optional),
		job_reference (InStoreReference, optional),
		regular_rate (BodhiCurrency, optional),
		overtime_rate (BodhiCurrency, optional),
		external_ids (Array[KeyValuePair], optional),
		store_id (string),
		ended_at (date-time, optional),
		shift_closed (boolean, optional),
		job_id (string, optional),
		started_at (date-time),
		overtime_minutes_worked (integer, optional),
		business_day (string, optional),
		total_minutes_worked (integer, optional),
		doubletime_rate (BodhiCurrency, optional)
}
````


**Timecard Embedded type definition**


````
TimecardBreak {
		start_time (date-time),
		end_time (date-time, optional),
		minutes (integer, optional),
		is_paid (boolean, optional),
		hourly_rate (string, optional)
}
InStoreReference {
		id (string),
		name (string, optional)
}
BodhiCurrency {
		code (object) = [''],
		value (integer),
		scale (integer, optional)
}
KeyValuePair {
		key (string),
		value (string, optional)
}
````




