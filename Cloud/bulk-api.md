
# Bulk API

The Bulk API is the prescribed method to post large data files to the platform. The API call is asynchronous and returns a key that the user must use to check the status of the import. 


## Use Case

You want to POST a large amount of data to the platform API. 
You have a JSON formatted file. Use the Platform /bulk API to POST the data.


##Prerequisites


* Write access to the data object you want to POST data to
* A text editor that can handle JSON files
* CURL or some other means to POST to the API


## Notes

1. The size limitation for the data file is 17 MB in one bulk post. The payload varies depending on the type of operation.
2. Update and upsert operations are only available for non-encapsulated types


## API definition


The bulk POST API is defined as follows:

````
https://<host>/<namespace>/bulk --data @jsonfile
````

Example

````
https://api.bodhi.space/mynamespace/bulk --data @myjsonfile.json
````




## JSON file format 

The JSON file consists of two tags 

* configuration for import
* the data payload

The configuration section specifies 

* the operation required - insert, update, upsert. ()Delete is not supported)
* whether a report is required - boolean
* the target data type


````
{
	"config": {
		"op": "insert" or "update" or "upsert"
		 "report": true,			<- optional, need a report? (default: false) 
		 "target": "target_name”	<- the name of the type
	},
	"payload": [
	{
		"name1": "value",
		"name2": "value"
	}, {
		"name1": "value",
		"name2": "value"
	}]
}
 
````


### Example JSON to bulk post multiple stores

````
{
	"config": {
		"op": "insert",
		"report": true,
		"target":  "Store"
	},
	"payload": [
		{
		"store_name": "Susans Scones",
		"store_number": "123456",
		"store_city": "San Francisco"
	    },
	    {
		"store_name": "Bobs Burgers",
		"store_number": "223456",
		"store_city": "San Francisco"
	    },
	    {
		"store_name": "Franks Franks",
		"store_number": "323456",
		"store_city": "San Francisco"
	    }
		]
}
````

## Using the API

You can use any language that support REST API calls and post the JSON document in the request. The following example is the simplest way to test the Bulk API using CURL and basic authentication. Note: As a best practice, you should use cookie based authentication in your applications to call the bulk API.


**Calling the API using CURL**

````
curl -is -X POST -H 'Content-type:application/json' -u u:p https://api.bodhi.space/ns/bulk --data @kpidef.json
````

**Result**

If you call the Bulk API from the command line you should see the following response once the command has executed successfully. The server returns a "202 Accepted".

If you do not see a HTTP status of "202 Accepted" the command has failed to execute. 


````
HTTP/1.1 202 Accepted
Server: nginx/1.8.0
Date: Thu, 21 Apr 2016 05:36:22 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 0
Connection: keep-alive
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: 
Access-Control-Allow-Methods: *
Access-Control-Allow-Origin: 
Access-Control-Expose-Headers: WWW-Authenticate, Server-Authorization, Location
bulk_id: ffffffff-0000-0000-0000-0fff000fFFFFF
Request-Time: 397
Set-Cookie: RUSK="GUID-username=NAME"; Path=/; Domain=.bodhi.space; Secure; HTTPOnly
````

In the report above, the property **bulk_id** represents the ID of the bulk job you have posted.  You will use  the bulk_id:<bulk report id> to check the status of your bulk POST.



## Checking the report

To check the status of the bulk post operation, use the bulk_id returned by the server when you posted your JSON payload.

The bulk GET API is defined as follows: 

````
GET /<namespace/bulk/<bulk_id>  
````

Example

````
https://api.bodhi.space/mynamespace/bulk/ffffffff-0000-0000-0000-0fff000fFFFFF

````  


Response codes

On running the operation you will receive one of the following:

HTTP Code | Description 
------------ | ------------- 
200 | job completed. with a json array body where the order of the cells matches the order of the payload. The report can be accessed only once. If the job failed during execution, the reason for the failure is provided in the response.  
204 | the report is not ready yet  
404 | no report was found with that id  





For errors or feedback with any of these workshops please contact support@hotschedules.com






