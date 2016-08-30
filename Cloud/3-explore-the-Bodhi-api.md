# Explore the HotSchedules IoT API


In this third workshop we will explore the Bodhi REST API. Rather than give a full explanation  of the API - it is recommended that you review the Bodhi API mechanics documentation located [here](http://docs.bodhi.space/#api-mechanics-tutorial). 

This workshop is intended to help you work with the Bodhi API and leverage the powerful query language capabilities of the Bodhi platform.  

The foundation for this document is the Mongo DB reference located at <http://docs.mongodb.org/manual/reference/operator/>.

Users may be unfamiliar with the REST query syntax. Those familiar with SQL should note that the same types of SQL query operations are possible using the REST API. Users wishing to understand the mapping between SQL queries (SELECT statements) and the Query syntax - should refer to the following document: <http://docs.mongodb.org/manual/reference/sql-comparison/>.


- [Prerequisites](#prereq)
- [The Bodhi API](#api)
- [Simple Queries using Browser](#browser)
- [Simple Queries using Bodhi CLI](#cli)
- [Using Query Selectors](#selectors)
- [Using the Aggregation API](#aggregate)




## <a name="prereq">Prerequisites</a>

To access the Bodhi API and execute the queries you will need the following:

1. A Bodhi account 
2. Any tool that can issue authenticated REST requests such as :
	- CURL command line
	- Bodhi Command Line Utility
	- Bodhi Query tool
	- Chrome browser and Postman 3rd party plugin for Chrome (note: Postman should only be used for queries and not for insert, update or delete operations).


## <a name="api">The Bodhi API</a>

The Bodhi API consists of four parts

- host
- namespace
- resource
- query

The host is the public URL of the Bodhi Cloud. This is <https://api.bodhi.space/>.
The namespace is the name of your Bodhi account or “tenant”. In this document we will assume our namespace is called “reveal” - an account that exists for the reveal chain of cafes located in the San Francisco Bay Area.
The resource is the name of the data structure (or “type”) that you want to access.  An example or a resource is SalesItem or SalesTransaction.

The query can be a simple request to get all results or a limited set of results using a where clause - or can be more complex and provide aggregated results. 
The results returned from a query, known as documents - and are returned in JSON notation.
API documentation for all Bodhi types - including any that you have created yourself, can be located at <https://api.bodhi.space/apidocs/index.html>





## <a name="browser">Simple Queries using the browser</a>

To test the following queries from the browser, first log into https://tools.bodhi.space with the account you want to make the REST queries with. This will ensure that any REST queries you make via the browser will be authenticated.


###Fetch Resources

Open a new browser tab.

To fetch all sales transactions from the type called 'SalesTransactions' - type the resource request below in your new browser tab. 

````
https://api.bodhi.space/reveal/resources/SalesTransaction
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction)


> Remember to change the namespace from 'reveal' to your namespace. For example, if your namespace was called 'joebloggs' your URL will look like this https://api.bodhi.space/**joebloggs**/resources/SalesTransaction



Once you press return, you should get the following result in the browser. It's unformatted JSON data.

![](images/k28.png "restAPI")

Try the following examples below:


**Fetch all store names**

````
https://api.bodhi.space/reveal/resources/Store?fields=name,sys_id
````

[Click to run]( https://api.bodhi.space/reveal/resources/Store?fields=name,sys_id ) (Change the namespace to match your account)


>The store name is used as a reference to sales transactions and sales items. We will use the store name in future examples.



**Fetch all sales transactions for January 24th 2015**

````
https://api.bodhi.space/reveal/resources/SalesTransaction?where={'business_day':'2015-01-24'}
````

[Click to run]( https://api.bodhi.space/reveal/resources/SalesTransaction?where={%27business_day%27:%272015-01-24%27} ) (Change the namespace to match your account)


**Fetch all sales transactions for Jan 24th 2015 for a specific store”**

> We will use the sys_id returned from our previous query

````
https://api.bodhi.space/reveal/resources/SalesTransaction?where={'business_day':'2015-01-24', 'store_id':'55a3fd3ddffa2e42a835e2ef'}
````

[Click to run]( https://api.bodhi.space/reveal/resources/SalesTransaction?where=%7B%27business_day%27:%272015-01-24%27,%27store_id%27:%2755a3fd3ddffa2e42a835e2ef%27%7D ) (Change the namespace, store name and date to match your data.)



**Fetch all sales transactions but return the 'Net Total' property only**

````
http://api.bodhi.space/reveal/resources/SalesTransaction?fields=net_total.value
````


[Click to run]( http://api.bodhi.space/reveal/resources/SalesTransaction?fields=net_total.value) (Change the namespace to match your data.)



**Fetch sales transactions for a specific store but return the 'Net Total' property only**

````
http://api.bodhi.space/reveal/resources/SalesTransaction?where={'business_day':'2015-01-24', 'store_id':'55a3fd3ddffa2e42a835e2ef'}&fields=net_total.value
````


[Click to run]( https://api.bodhi.space/reveal/resources/SalesTransaction?where=%7B%27business_day%27:%272015-01-24%27,%27store_id%27:%2755a3fd3ddffa2e42a835e2ef%27%7D&fields=net_total.value) (Change the namespace to match your data.)




### Count resources

The count API returns the number of document instances in a collection - or matching a query provided. To count the instances in a collection, use the **resources/resourcename/count** API.

**Count all sales transactions**

````
https://api.bodhi.space/reveal/resources/SalesTransaction/count
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/count)  (Change the namespace to match your data.)



**Count all sales transactions for a specific store**

````
http://api.bodhi.space/reveal/resources/SalesTransaction/count?where={'store_id':'55a3fd3ddffa2e42a835e2ef'}
````

[Click to run]( https://api.bodhi.space/reveal/resources/SalesTransaction/count?where=%7B%27store_id%27:%2755a3fd3ddffa2e42a835e2ef%27%7D ) (Change the namespace, store name and date to match your data.)



**Count all sales transactions for a specific store on the 24th January 2015.**

````
http://api.bodhi.space/reveal/resources/SalesTransaction/count?where={'business_day':'2015-01-24', 'store_id':'55a3fd3ddffa2e42a835e2ef'}
````

[Click to run]( https://api.bodhi.space/reveal/resources/SalesTransaction/count?where=%7B%27business_day%27:%272015-01-24%27,%27store_id%27:%2755a3fd3ddffa2e42a835e2ef%27%7D ) (Change the namespace, store name and date to match your data.)




## <a name="cli">Simple Queries using Bodhi CLI</a>

You can make the same REST queries using the Bodhi CLI.  

**bodhi-cli** is a command line tool, that allows app developers to quickly work with the cloud API to create and manage data types and work with the data stored in those types.

Open your command prompt (select to run as Administrator on Windows)
Follow the instructions located here: <http://docs.bodhi.space/#bodhi-command-line-interface>

Follow the instructions to set up a Bodhi project folder using **bodhi init** and set up your **rbc_project.json** file with the environment variables to access your namespace with your credentials. You should read the docs but the steps are as follows:


````
npm install -g bodhi-cli
mkdir bodhiapps
cd bodhiapps
bodhi init  /path/to/new/project/root
bodhi new my_environment_name
bodhi set-default my_environment_name

````

This will create a working folder on your machine and set the CLI to default to your namespace. 

**Example**

Assume our namespace is called 'baybridge' and we want to set up the CLI to use that namespace without having to specify those details every time we wish to converse with the cloud.

````
npm install -g bodhi-cli
mkdir bodhiapps
cd bodhiapps
bodhi init  bodhiapps
bodhi new baybridge -s api.bodhi.space -n baybridge -u susanjones -p ABCDE
bodhi set-default baybridge

````

Once installed, the bodhi-cli can be accessed by typing 'bodhi' at the command line. Enter **bodhi --help** to get a full list of the CLI features.

All resource requests take the following structure:

````
bodhi [options] resources/:resource-name/[:id][?:query] “”
````
Where options are

- get
- count
- post
- put
- post
- delete


**Fetch Resources**

Reading a collection of Resources

Our first query will attempt to extract all the resources in a given collection using the get action.

````
bodhi get resources/MyResource
````


**Counting Resources**

````
bodhi get resources/MyResource/count
````


The CLI exposes a shorthand for this command using the count action.

````
bodhi count resources/MyResource
````


**Fetch a Resource by ID**

Fetch by unique Attribute

````
bodhi get resources/MyResource/:id
````





# <a name="selectors">Using Query Selectors</a>


Bodhi API supports the use of standard query operators. 


**Comparison operators**

Operator | Description | 
------------ | ------------- | ------------
$eq | Matches values that are equal to a specified value.  | 
$gt | Matches values that are greater than a specified value.  | 
$gte | Matches values that are greater than or equal to a specified value.
$lt | Matches values that are less than a specified value.
$lte | Matches values that are less than or equal to a specified value.
$ne | Matches all values that are not equal to a specified value.
$in | Matches any of the values specified in an array.
$nin | Matches none of the values specified in an array.

	
**Logical Operators**

Operator | Description | 
------------ | ------------- | ------------
$or | Joins query clauses with a logical OR returns all documents that match the conditions of either clause.
$and | Joins query clauses with a logical AND returns all documents that match the conditions of both clauses.
$not | Inverts the effect of a query expression and returns documents that do not match the query expression.
$nor | Joins query clauses with a logical NOR returns all documents that fail to match both clauses.

**Element**

Operator | Description | 
------------ | ------------- | ------------
$exists | Matches documents that have the specified field.
$type | Selects documents if a field is of the specified type.


**Evaluation**

Operator | Description | 
------------ | ------------- | ------------
$mod | Performs a modulo operation on the value of a field and selects documents with a specified result.
$regex | Selects documents where values match a specified regular expression.
$text | Performs text search.
$where | Matches documents that satisfy a JavaScript expression.

**Geospatial**

Operator | Description | 
------------ | ------------- | ------------
$geoWithin | Selects geometries within a bounding GeoJSON geometry. The 2dsphere and 2d indexes support $geoWithin.
$geoIntersects | Selects geometries that intersect with a GeoJSON geometry. The 2dsphere index supports $geoIntersects.
$near | Returns geospatial objects in proximity to a point. Requires a geospatial index. The 2dsphere and 2d indexes support $near.
$nearSphere | Returns geospatial objects in proximity to a point on a sphere. Requires a geospatial index. The 2dsphere and 2d indexes support $nearSphere.

**Array**

Operator | Description | 
------------ | ------------- | ------------
$all | Matches arrays that contain all elements specified in the query.
$elemMatch | Selects documents if element in the array field matches all the specified $elemMatch conditions.
$size | Selects documents if the array field is a specified size.

**Projection Operators**

Operator | Description | 
------------ | ------------- | ------------
$ | Projects the first element in an array that matches the query condition.
$elemMatch | Projects the first element in an array that matches the specified $elemMatch condition.
$slice | Limits the number of elements projected from an array. Supports skip and limit slices.

## Query Selector Examples

NOTE: All API request submitted should be posted as one line, not broken out with carriage returns as shown here (for clarity).

**Get all SalesTransactions after a certain date**

````
https://api.bodhi.space/reveal/resources/SalesTransaction?where={'sys_created_at':{$gte:{'$date':'2015-07-25T00:00:00.000Z'}}}
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction?where={%27sys_created_at%27:{$gte:{%27$date%27:%272015-07-25T00:00:00.000Z%27}}}) ( Change the namespace and date to match your data.)




**Get all AlohaTimeCard entries where overtime pay is greater than or equal to one dollar and display only the overtime pay and the date**

````
https://api.bodhi.space/reveal/resources/AlohaTimeCard?where={"OVERPAY":{$gte: 1}}&fields=OVERPAY,DATE
````

[Click to run](https://api.bodhi.space/reveal/resources/AlohaTimeCard?where={%27OVERPAY%27:{$gte: 1}}&fields=OVERPAY,DATE )  (Change the namespace, type name and fields to match your data. (Check you are using Aloha as the types might exist in your environment...))





# <a name="aggregate">Using the Aggregation API</a>

Bodhi API supports the use of aggregation to return a result set with aggregated totals. 

The aggregation framework is based on pipeline concept, just like a Unix pipeline. There can be N number of operators. The output of the first operator will be passed as an input to the second operator. The output of second operator will be passed as input to the third operator and so on.

You can create variables to store the results of your operations at each stage of the pipeline, and then use those variables in subsequent operations.

## Pipeline order of precedence

The following example, the aggregation pipeline consists of a $group stage, a $sort stage, another $group stage, and a $project stage. The example shown illustrates the use of several pipeline operators to return the smallest and largest cities by population for each state. The example is generic to illustrate the use case (it is not associated with a type).


````
aggregate( [
   { $group:
      {
        _id: { state: "$state", city: "$city" },
        pop: { $sum: "$pop" }
      }
   },
   { $sort: { pop: 1 } },
   { $group:
      {
        _id : "$_id.state",
        biggestCity:  { $last: "$_id.city" },
        biggestPop:   { $last: "$pop" },
        smallestCity: { $first: "$_id.city" },
        smallestPop:  { $first: "$pop" }
      }
   },

  // the following $project is optional, and
  // modifies the output format.

  { $project:
    { _id: 0,
      state: "$_id",
      biggestCity:  { name: "$biggestCity",  pop: "$biggestPop" },
      smallestCity: { name: "$smallestCity", pop: "$smallestPop" }
    }
  }
] )
````

**1st Group stage**

The first $group stage groups the documents by the combination of the city and state, calculates the sum of the population values for each combination, and outputs a document for each city and state combination.

At this stage in the pipeline, the documents resemble the following:

````
{
  "_id" : {
    "state" : "CA",
    "city" : "SAN FRANCISCO"
  },
  "pop" : 849774
}
````

**Sort stage**

The $sort stage orders the documents in the pipeline by the pop field value, from smallest to largest; i.e. by increasing order. This operation does not alter the documents.


**2nd Group stage**

The next $group stage groups the now-sorted documents by the _id.state field (i.e. the state field inside the _id document) and outputs a document for each state.
The stage also calculates the following four fields for each state. Using the $last expression, the $group operator creates the biggestCity and biggestPop fields that store the city with the largest population and that population. Using the $first expression, the $group operator creates the smallestCity and smallestPop fields that store the city with the smallest population and that population.
The documents, at this stage in the pipeline, resemble the following:

````
{
  "_id" : "CA",
  "biggestCity" : "LOS ANGELES",
  "biggestPop" : 3885000,
  "smallestCity" : "VERNON",
  "smallestPop" : 112
}
````

**Project stage**

The final $project stage renames the _id field to state and moves the biggestCity, biggestPop, smallestCity, and smallestPop into biggestCity and smallestCity embedded documents.
The output documents of this aggregation operation resemble the following:

````
{
  "state" : "CA",
  "biggestCity" : {
    "name" : "LOS ANGELES",
    "pop" : 3885000
  },
  "smallestCity" : {
    "name" : "VERNON",
    "pop" : 112
  }
}
````




## Pipeline Operators

Operator | Description | 
------------ | ------------- | ------------
$project | Reshapes each document in the stream, such as by adding new fields or removing existing fields. For each input document, outputs one document.
$match | Filters the document stream to allow only matching documents to pass unmodified into the next pipeline stage. $match uses standard MongoDB queries. For each input document, outputs either one document (a match) or zero documents (no match).
$redact | Reshapes each document in the stream by restricting the content for each document based on information stored in the documents themselves. Incorporates the functionality of $project and $match. Can be used to implement field level redaction. For each input document, outputs either one or zero document.
$limit | Passes the first n documents unmodified to the pipeline where n is the specified limit. For each input document, outputs either one document (for the first n documents) or zero documents (after the first n documents).
$skip | Skips the first n documents where n is the specified skip number and passes the remaining documents unmodified to the pipeline. For each input document, outputs either zero documents (for the first n documents) or one document (if after the first n documents).
$unwind | Deconstructs an array field from the input documents to output a document for each element. Each output document replaces the array with an element value. For each input document, outputs n documents where n is the number of array elements and can be zero for an empty array.
$sort | Reorders the document stream by a specified sort key. Only the order changes; the documents remain unmodified. For each input document, outputs one document.
$geoNear | Returns an ordered stream of documents based on the proximity to a geospatial point. Incorporates the functionality of $match, $sort, and $limit for geospatial data. The output documents include an additional distance field and can include a location identifier field.
$out | Writes the resulting documents of the aggregation pipeline to a collection. To use the $out stage, it must be the last stage in the pipeline.









**Get the total sales by store to date**

````
https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$store_id',totalSales:{$sum:'$tender_total.value'}}}}]
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$store_id',totalSales:{$sum:'$tender_total.value'}}}])  (Change the namespace to match your account)


**Get the number of Sales Transactions per store to date**

````
https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$store_id',countOfSales: {$sum: 1}}}]
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$store_id',countOfSales:{$sum:1}}}])  (Change the namespace to match your account)


**Get the number of Sales Items sold per store to date**

````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$store_id',countOfSales: {$sum: 1}  }}]
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$store_id',countOfSales:{$sum:1}}}])  (Change the namespace to match your account)


**Get the number of Sales Items sold per day for all stores combined**

````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$business_day',countOfSales:{$sum: 1}}}]
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$business_day',countOfSales:{$sum:1}}}])  (Change the namespace to match your account)

**Get sales totals and sales counts for each business day**

````
https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$business_day', totalSales:{$sum:'$tender_total.value'}, countOfSales: {$sum: 1} }}]
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$business_day',totalSales:{$sum:'$tender_total.value'},countOfSales:{$sum:1}}}])  (Change the namespace to match your account)

###Get average values

**Get sales totals and sales counts for each business day and determine the average sales per day**

````
https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=
	[{$group:{_id:'$business_day', 
				totalSales:{$sum:'$tender_total.value'},
				countOfSales: {$sum: 1}}},
	 {$project:{average: {$divide: [ "$totalSales", "$countOfSales" ]}}} ] 
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$business_day',totalSales:{$sum:'$tender_total.value'},countOfSales:{$sum:1}}},{$project:{average:{$divide:["$totalSales","$countOfSales"]}}}] )  (Change the namespace to match your account)


**Get average sales per day using the $avg operator**

````
https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=
[{
     $group:{_id:'$business_day',  
                averageSales: { 
                                $avg: '$tender_total.value'
                            } 
            }
}] 
````

[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$business_day',averageSales:{$avg:'$tender_total.value'}}}])  (Change the namespace to match your account)


**Get average sales by zip code**             

````
https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=
[{
            $group:{_id:'$Post_Code', 
                         averageSalesbyPostCode:{
                                                 $avg:'$Actual_Sales'
                                                }
            }
}]
````



[Click to run](https://api.bodhi.space/reveal/resources/SalesTransaction/aggregate?pipeline=[{$group:{_id:'$Post_Code', avgsales:{$avg:'$Actual_Sales'}}}])  (Change the namespace to match your account)


**Get sales totals for business day of all items**


````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=
[{
   $group:{
           _id:'$business_day', 
           totalSales:{
                       $sum:'$net_total.value'
                      },
           countOfSales: {
                          $sum: 1} 
                         }
}]
````


[Click to run](
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$business_day', totalSales:{$sum:'$net_total.value'},countOfSales: {$sum: 1} }}])  (Change the namespace to match your account)



**Get sales totals for business day of all items for a specific day**


````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{ $match: { business_day: "2015-07-22" } }
{$group:{_id:'$business_day', 
totalSales:{$sum:'$net_total.value'},
countOfSales: {$sum: 1} }}]
````


[Click to run](https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{ $match: { business_day: "2015-07-22" } }
{$group:{_id:'$business_day', 
totalSales:{$sum:'$net_total.value'},
countOfSales: {$sum: 1} }}])  (Change the namespace to match your account)


**Get sales totals for business day of all items and create a list of the items sold on that day across all stores**


````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{$group:{_id:'$business_day', 
totalSales:{$sum:'$net_total.value'},
countOfSales: {$sum: 1}, 
category: { $addToSet: "$description" } }}]
````


[Click to run]( https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$business_day',totalSales:{$sum:'$net_total.value'},countOfSales:{$sum: 1},category:{$addToSet:"$description"}}}] )  (Change the namespace to match your account)


**Get sales items by day, sum totals and sort by day**

````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{$group:{_id:'$business_day', 
totalSales:{$sum:'$net_total.value'},
countOfSales: {$sum: 1}, 
category: { $addToSet: "$description" } }}]&{$sort:{ business_day: 1 }}
````


[Click to run]( https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$business_day',totalSales:{$sum:'$net_total.value'},countOfSales:{$sum:1},category:{$addToSet:"$description"}}}]&{$sort:{business_day:1}})  (Change the namespace to match your account)

**Get total pay by day and number of payments made**

````
https://api.bodhi.space/reveal/resources/AlohaTimeCard/aggregate?
pipeline=[{$group:{_id:'$DATE', totalPay:{$sum:'$PAY'}, countpay: {$sum: 1} }}]
````


[Click to run]( https://api.bodhi.space/reveal/resources/AlohaTimeCard/aggregate?pipeline=[{$group:{_id:'$DATE',totalPay:{$sum:'$PAY'},countpay:{$sum:1}}}])  (Change the namespace to match your account)

**Get overtime and Credit card tips earned by day** 


````
https://api.bodhi.space/reveal/resources/AlohaTimeCard/aggregate?
pipeline=[{$group:{_id:'$DATE', totalPay:{$sum:'$PAY'}, 
overtime_mins:{$sum:'$OVERMIN'}, 
CCtips:{$sum:'$CCTIPS'}, countpay: {$sum: 1} }}]
````


[Click to run](https://api.bodhi.space/reveal/resources/AlohaTimeCard/aggregate?pipeline=[{$group:{_id:'$DATE',totalPay:{$sum:'$PAY'},overtime_mins:{$sum:'$OVERMIN'},CCtips:{$sum:'$CCTIPS'},countpay:{$sum:1}}}])  (Change the namespace to match your account)


**Get total sales of each item sold and display the product name and category**

````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{$group:{_id:'$description', 
cat: {$sum:'sales_category.name'}, 
totalSales:{$sum:'$quantity'}}}]
````

[Click to run]( https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$description',cat:{$sum:'sales_category.name'},totalSales:{$sum:'$quantity'}}}])  (Change the namespace to match your account)

**Get total sales by product category** 

````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{$group:{_id:'$sales_category.name', totalSales:{$sum:'$quantity'}}}]
````

[Click to run]( https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$group:{_id:'$sales_category.name',totalSales:{$sum:'$quantity'}}}])  (Change the namespace to match your account)


**Get total sales of any item of type Food**

````
https://api.bodhi.space/reveal/resources/SalesItem/aggregate?
pipeline=[{ $match: { sales_category.name: "Food" } },
{$group:{_id:'$description', totalSales:{$sum:'$quantity'} }}]
````


[Click to run](https://api.bodhi.space/reveal/resources/SalesItem/aggregate?pipeline=[{$match:{sales_category.name:"Food"}},{$group:{_id:'$description',totalSales:{$sum:'$quantity'}}}])  (Change the namespace to match your account)



 