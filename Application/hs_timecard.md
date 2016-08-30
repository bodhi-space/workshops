# Timecard Service Methods



## Get Timecards

**Method Name:** getTimeCardsThis method returns an array of Timecards for a specific date range.
Each timecard represents one employee punch record, including business date, regular and overtime minutes, wages, clock in and clock out times. 
If this store is using HotSchedules' webbased timeclock for employee clockin, any open punches in the date range are also included in the response.
This method takes in a concept ID, store ID, start and end dates. 


### Request


````
/concept/store/getTimeCards?
start_day=DD&
start_month=MM&
start_year=YYYY&
end_day=DD&
end_month=MM&
end_year=YYYY
````


Property | Primitive | 
------------ | ------------- | 
start_day | Integer  | start_month  | Integer | 
start_year | Integer | 
end_day | Integer | 
end_month | Integer | 
end_year | Integer | 


#### Response


Response | Primitive | 
------------ | ------------- | 
  jobName | String | 
  ovtTtl | Real | 
  ovtHrs | Integer | 
  clockOut | UTC DateTime | 
  regWage | Real | 
  clockIn | UTC DateTime | 
  ovtWage | Real | 
  breakMinutes | Real | 
  businessDate | compound type (see below)
  jobId | Integer | 
  regHrs | Real | 
  spcTtl | Real | 
  hsId | Integer | 
  spcHrs | Integer | 
  ovtMins | Integer | 
  storeNum | Integer | 
  empPosId | Integer | 
  regTtl | Real
  

 
businessDate | Primitive | 
------------ | ------------- | 
    month | Integer | 
    year | Integer | 
    day | Integer
      


**Example Response**

````
{
  "jobName": "Cook",
  "ovtTtl": 0,
  "ovtHrs": 0,
  "clockOut": "2016-07-31T22:05:00-05:00",
  "regWage": 9,
  "clockIn": "2016-07-30T15:56:00-05:00",
  "ovtWage": 13.5,
  "breakMinutes": 0,
  "jobId": 16921407,
  "businessDate": {
    "month": 7,
    "year": 2016,
    "day": 31
  },
  "regHrs": 6.15,
  "spcTtl": 0,
  "hsId": 929931334634,
  "spcHrs": 0,
  "ovtMins": 0,
  "storeNum": 1,
  "empPosId": 1052,
  "regTtl": 55.35
}
````#### cURL Request 


````
curl -X GET -H "Content-Type:application/json" 
-u username:password 
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules
/1/1/getTimeCards?
start_day=30&
start_month=4&
start_year=2016&
end_day=5&
end_month=5&
end_year=2016"
````




## Set Timecards

**Method Name:** setTimeCardsV3This method inserts an array of Timecards for a specific date range.
Each timecard represents one employee punch record, including business date, regular and overtime minutes, wages, clock in and clock out times. 
This method takes in a concept ID, store ID, start date, end date and an array of Timecard objects. 


### Request


````
/concept/store/setTimeCardsV3?
start_day=DD&
start_month=MM&
start_year=YYYY&
end_day=DD&
end_month=MM&
end_year=YYYY&
[{
  "jobName": String,
  "ovtTtl": Real,
  "ovtHrs": Integer,
  "clockOut": UTC DateTime,
  "regWage": Real,
  "clockIn": UTC DateTime,
  "ovtWage": Real,
  "breakMinutes": Real,
  "jobId": Integer,
  "businessDate": {
    "month": Integer,
    "year": Integer,
    "day": Integer
  },
  "regHrs": Real,
  "spcTtl": Real,
  "hsId": Integer,
  "spcHrs": Integer,
  "ovtMins": Integer,
  "storeNum": Integer,
  "empPosId": Integer,
  "regTtl": Real
}]
````


Property | Primitive | 
------------ | ------------- | 
start_day | Integer  | start_month  | Integer | 
start_year | Integer | 
end_day | Integer | 
end_month | Integer | 
end_year | Integer | 



Timecard property | Primitive | 
------------ | ------------- | 
jobName | String | 
ovtTtl | Real | 
ovtHrs | Integer | 
clockOut | UTC DateTime | 
regWage | Real | 
clockIn | UTC DateTime | 
ovtWage | Real | 
breakMinutes | Real | 
businessDate | compound type (see below)
jobId | Integer | 
regHrs | Real | 
spcTtl | Real | 
hsId | Integer | 
spcHrs | Integer | 
ovtMins | Integer | 
storeNum | Integer | 
empPosId | Integer | 
regTtl | Real
  
 
businessDate | Primitive | 
------------ | ------------- | 
month | Integer | 
year | Integer | 
day | Integer
      


#### cURL Request 

````
curl -X PUT -H "Content-Type:application/json" 
-u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules
/1/1/setTimeCardsV3?
start_day=30&
start_month=4&
start_year=2016&
end_day=5&
end_month=5&
end_year=2016" 
-d "[{
  "jobName": "Cook",
  "ovtTtl": 0,
  "ovtHrs": 0,
  "clockOut": "2016-07-31T22:05:00-05:00",
  "regWage": 9,
  "clockIn": "2016-07-30T15:56:00-05:00",
  "ovtWage": 13.5,
  "breakMinutes": 0,
  "jobId": 16921407,
  "businessDate": {
    "month": 7,
    "year": 2016,
    "day": 31
  },
  "regHrs": 6.15,
  "spcTtl": 0,
  "hsId": 929931334634,
  "spcHrs": 0,
  "ovtMins": 0,
  "storeNum": 1,
  "empPosId": 1052,
  "regTtl": 55.35
}]"
````



#### To Document 

getTimeCardsDeclaredTips - does not seem to be implemented   
setTimeCardsDeclaredTips - document  

curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"

