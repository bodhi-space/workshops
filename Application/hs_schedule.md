# Schedules and Shifts[Get schedules](https://github.com/bodhi-space/workshops/blob/master/Application/hs_schedule.md#get-schedules)     
[Get shifts](https://github.com/bodhi-space/workshops/blob/master/Application/hs_schedule.md#get-shifts)

## Get Schedules

**Method Name:** getScheduleThis method returns returns an array of scheduled shifts for a specific date range 

This method takes in a concept ID, store ID, start and end dates.


### Request

````
/concept/store/getSchedule?
start_day=DD&
start_month=MM&
start_year=YYYY&
end_day=DD&
end_month=MM&
end_year=YYYY
````


Property | Primitive | 
------------ | ------------- | 
concept ID | Integer  | 
start_day | Integer  | start_month  | Integer | 
start_year | Integer | 
end_day | Integer | 
end_month | Integer | 
end_year | Integer | 



### Response



Response | Primitive | 
------------ | ------------- | 
outDate |  SimpleDate | 
jobHsId |  Integer | 
payRate |  Real | 
inDate |  SimpleDate | 
specialPay |  Integer | 
empHSId |  Integer | 
ovtMinutes |  Integer | 
inTime |  SimpleTime | 
jobPosId |  Integer | 
weekStart |  SimpleDate | 
ovtRate |  Integer | 
regMinutes |  Integer | 
locationId |  Integer | 
weekEnd |  SimpleDate | 
outTime |  SimpleTime | 
scheduleId |  Integer | 
empPosId |  Integer  | 



SimpleDate | Primitive | 
------------ | ------------- | 
month |  Integer | 
year |  Integer | 
day |  Integer  | 


SimpleTime | Primitive | 
------------ | ------------- | 
hours |  Integer | 
seconds |  Integer | 
militaryTime |  true | 
minutes |  Integer  | 


**Example Response**

```
  [{
    "outDate": {
      "month": 5,
      "year": 2016,
      "day": 3
    },
    "jobHsId": 786323136,
    "payRate": 9.5,
    "inDate": {
      "month": 5,
      "year": 2016,
      "day": 2
    },
    "specialPay": 0,
    "empHSId": 4177284,
    "ovtMinutes": 0,
    "inTime": {
      "hours": 4,
      "seconds": 0,
      "militaryTime": true,
      "minutes": 0
    },
    "jobPosId": 22,
    "weekStart": {
      "month": 5,
      "year": 2016,
      "day": 2
    },
    "ovtRate": 0,
    "regMinutes": 1200,
    "locationId": -1,
    "weekEnd": {
      "month": 5,
      "year": 2016,
      "day": 8
    },
    "outTime": {
      "hours": 0,
      "seconds": 0,
      "militaryTime": true,
      "minutes": 0
    },
    "scheduleId": 781691539,
    "empPosId": 4027
  },]
```

#### cURL Request 

````
curl -X GET -H "Content-Type:application/json" 
-u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getScheduleV3?
start_day=30&
start_month=4&
start_year=2016&
end_day=5&
end_month=5&
end_year=2016"
````




## Get Shifts


**Method Name:** getShiftsV3This method returns returns an array of scheduled shifts for a specific date range, shift type and status.

This method takes in a concept ID, store ID, start and end dates.


### Request

````
/concept/store/getShiftsV3?
start_day=DD&
start_month=MM&
start_year=YYYY&
end_day=DD&
end_month=MM&
end_year=YYYY&
is_house=true/false&
is_scheduled=true/false&
is_posted=true/false
````


Property | Primitive | 
------------ | ------------- | 
concept ID | Integer  | 
start_day | Integer  | start_month  | Integer | 
start_year | Integer | 
end_day | Integer | 
end_month | Integer | 
end_year | Integer | 
is_house | Boolean | 
is_scheduled | Boolean | 
is_posted | Boolean | 



### Response



Response | Primitive | 
------------ | ------------- | 
outDate |  SimpleDate | 
jobHsId |  Integer | 
payRate |  Real | 
inDate |  SimpleDate | 
specialPay |  Integer | 
empHSId |  Integer | 
ovtMinutes |  Integer | 
inTime |  SimpleTime | 
jobPosId |  Integer | 
weekStart |  SimpleDate | 
ovtRate |  Integer | 
regMinutes |  Integer | 
locationId |  Integer | 
weekEnd |  SimpleDate | 
outTime |  SimpleTime | 
scheduleId |  Integer | 
empPosId |  Integer  | 



SimpleDate | Primitive | 
------------ | ------------- | 
month |  Integer | 
year |  Integer | 
day |  Integer  | 


SimpleTime | Primitive | 
------------ | ------------- | 
hours |  Integer | 
seconds |  Integer | 
militaryTime |  true | 
minutes |  Integer  | 


**Example Response**

```
  [{
    "outDate": {
      "month": 5,
      "year": 2016,
      "day": 3
    },
    "jobHsId": 786323136,
    "payRate": 9.5,
    "inDate": {
      "month": 5,
      "year": 2016,
      "day": 2
    },
    "specialPay": 0,
    "empHSId": 4177284,
    "ovtMinutes": 0,
    "inTime": {
      "hours": 4,
      "seconds": 0,
      "militaryTime": true,
      "minutes": 0
    },
    "jobPosId": 22,
    "weekStart": {
      "month": 5,
      "year": 2016,
      "day": 2
    },
    "ovtRate": 0,
    "regMinutes": 1200,
    "locationId": -1,
    "weekEnd": {
      "month": 5,
      "year": 2016,
      "day": 8
    },
    "outTime": {
      "hours": 0,
      "seconds": 0,
      "militaryTime": true,
      "minutes": 0
    },
    "scheduleId": 781691539,
    "empPosId": 4027
  },]
```

#### cURL Request 

````
curl -X GET -H "Content-Type:application/json" 
-u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getShiftsV3?
start_day=30&
start_month=4&
start_year=2016&
end_day=5&
end_month=5&
end_year=2016"&
is_house=true&
is_scheduled=true&
is_posted=true"
````