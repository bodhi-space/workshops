# Store Service

[Get stores](https://github.com/bodhi-space/workshops/blob/master/Application/hs_org.md#get-stores)    
[Get groups](https://github.com/bodhi-space/workshops/blob/master/Application/hs_org.md#get-groups-for-a-concept)    



## Get Stores

**Method Name:** getStores



### Request

````
/concept/getStores?group_id=0
````


Property | Primitive | Definition
------------ | ------------- | ------------
concept ID | Integer  | 


### Response

An array of stores.

Response | Primitive | 
------------ | ------------- | 
groupName |  String | 
active |  Boolean | 
groupExtId |  Integer | 
storeName |  String | 
storeNum |  Integer |  
    

**Example response**
    

````
{
    "groupName": "Tiffles",
    "active": true,
    "groupExtId": 1,
    "storeName": "Tiffles San Francisco",
    "storeNum": 2
 }
````



### cURL Request

```
curl -X GET -H "Content-Type:application/json" 
-u username:pasword 
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/getStores?group_id=0"
```





## Get Groups for a concept

**Method Name:** getGroups



### Request

````
/concept/getGroups
````


Property | Primitive | 
------------ | ------------- | 
concept ID | Integer  | 


### Response



Response | Primitive | 
------------ | ------------- | 
name | String | 
extId | Integer | 
conceptExtId | Integer | 


**Example Response**

```
  [{
    "name": "Tiffles Corporate Catering",
    "extId": 0,
    "conceptExtId": 1
  }]
```



````
curl -X PUT -H "Content-Type:application/json" 
-u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/getGroups
````