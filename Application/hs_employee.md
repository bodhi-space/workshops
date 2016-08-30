
# Employee Service Methods



[Get all employees for a store](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#get-all-employees-for-a-store)  
[Get all employee jobs for a store](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#get-all-employee-jobs-for-a-store)  
[Get all jobs defined at a store](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#get-all-jobs-defined-for-a-store)  
[Get employee availability](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#get-employee-availability)  
[Get all employees assigned to a schedule](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#get-all-employees-assigned-to-a-schedule)  
[Add employees to a store](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#add-employees-to-a-store)  
[Assign jobs to employees](https://github.com/bodhi-space/workshops/blob/master/Application/hs_employee.md#assign-jobs-to-employees-in-a-store)  




## Get All Employees for a Store

**Method Name:** getStoreEmployees

This method takes in a concept ID, store ID, a flag to return 

### Request


````
/concept/store/getStoreEmployees?active_only=BOOLEAN
````


#### Response


Response | Primitive | 
------------ | ------------- | 
zipCode | Integer  | 
address | String | 
clientId | Integer  | 
address2 | String | 
city | String  | 
NName | String | 
altId | Integer  | 
empNum | Integer | 
phone | String  | 
dob | UTC | 
state | String  | 
email | String | 
status | Integer | 

**Example Response**

````
[
  {
    "zipCode": "",
    "hireDate": "2012-05-04T17:00:14.590-05:00",
    "address": "",
    "clientId": 14935377,
    "LName": "Perkins",
    "address2": "",
    "city": "",
    "mobile": "",
    "NName": "",
    "altId": -1,
    "FName": "Norbert",
    "empNum": -1,
    "phone": "no number",
    "hsId": 3190170,
    "dob": "1971-12-07T00:00:00-06:00",
    "state": "",
    "storeNum": 2,
    "email": "",
    "status": 1
  },
]
````




```
curl -X GET -H "Content-Type:application/json" -u username:password 
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules
/1/1/getStoreEmployees?active_only=true"
```






## Get All Employee Jobs for a Store

**Method Name:** getEmpJobs

Get a list of all jobs assigned to all employees for a store.  
Takes a concept ID and a store ID and returns an array of Employee Job objects. 

### Request


````
/concept/store/getEmpJobs?active_only=BOOLEAN
````



Property | Primitive | Definition
------------ | ------------- | ------------
concept | Integer  | The identifier for the location's concept.
active_only | Boolean | Include terminated employees in the response?


### Response


Response | Primitive | 
------------ | ------------- | 
hsJobId | Integer  | 
regWage | Real | 
posEmpId | Integer  | 
storeNum | Integer | 
ovtWage | Real  | 
primary | Boolean | 


**Example Response**

````
[
  {
    "hsJobId": 8965542,
    "clientId": 14935377,
    "regWage": 8.8,
    "posEmpId": 4001,
    "hsEmpId": 4177257,
    "storeNum": 2,
    "ovtWage": 13.200001,
    "posJobId": 18,
    "primary": false
  }
]
````

```
curl -X GET -H "Content-Type:application/json" -u username:password 
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules
/1/1/getEmpJobs?active_only=true
```


## Get all jobs defined for a Store

**Method Name:** getStoreJobs

This method takes in a concept ID, store ID, a flag to return 

### Request


````
/concept/store/getStoreJobs?active_only=BOOLEAN
````


Property | Primitive | Definition
------------ | ------------- | ------------
concept | Integer  | The identifier for the location's concept.
active_only | Boolean | Include only active jobs in the response?


#### Response


Response | Primitive | 
------------ | ------------- | 
jobName | String  | 
clientId | Integer | 
hsId | Integer  | 
storeNum | Integer | 


**Example Response**

````
[
  {
    "jobName": "Bartender",
    "posId": 18,
    "clientId": 14935377,
    "hsId": 786323127,
    "defRate": 8.7,
    "storeNum": 2
  }
]
````




```
curl -X GET -H "Content-Type:application/json" -u username:password
 "https://api.bodhi.space/namespace/controllers/vertx/hotschedules
 /1/1/getStoreJobs?active_only=true"
```






## Get Employee availability

**Method Name:** getEmpAvailability

This method takes in a concept ID and a store ID and returns an

### Request


````
/concept/store/getEmpAvailability?active_only=BOOLEAN
````


Property | Primitive | Definition
------------ | ------------- | ------------
concept | Integer  | The identifier for the location's concept.
active_only | Boolean | Include only active jobs in the response?


#### Response


Response | Primitive | 
------------ | ------------- | 
empNum | Integer  | 

availability definition:
------------ | ------------- | 
parHoursMax | Integer | 
parShiftsMax | Integer  | 
shiftName | String | 
parHoursMin | Integer  | 
dayName | String | 
partialBeforeAfter | String  | 
dayNum | Integer |
partialTime  | String | 
statusNum | Integer |

**Example Response**

````
[
  {
    "empNum": -1,
    "availabilities": [
      {
        "parHoursMax": -1,
        "parShiftsMax": -1,
        "shiftId": 781691596,
        "shiftName": "AM",
        "parHoursMin": -1,
        "parShiftsMin": -1,
        "dayName": "Saturday",
        "partialBeforeAfter": "",
        "statusName": "Not Available",
        "dayNum": 7,
        "partialTime": "",
        "statusNum": 3
      },
      {
        "parHoursMax": -1,
        "parShiftsMax": -1,
        "shiftId": 781691610,
        "shiftName": "PM",
        "parHoursMin": -1,
        "parShiftsMin": -1,
        "dayName": "Saturday",
        "partialBeforeAfter": "",
        "statusName": "Not Available",
        "dayNum": 7,
        "partialTime": "",
        "statusNum": 3
      }
    ],
    "empHrId": -1
  },
]
````



````
curl -X GET -H "Content-Type:application/json" -u username:password
 "https://api.bodhi.space/namespace/controllers/vertx/hotschedules
 /1/1/getEmpAvailability?active_only=true"
````




## Get all Employee's assigned to a schedule

**Method Name:** getEmpInfo

This method returns a list of all employees assigned to a schedule for a store. Takes in a concept ID and a store ID and returns an array of people assigned to a schedule.

### Request


````
/concept/store/getEmpInfo?active_only=BOOLEAN
````


Property | Primitive | Definition
------------ | ------------- | ------------
concept | Integer  | The identifier for the location's concept.
active_only | Boolean | Include only active jobs in the response?


#### Response


Response | Primitive | 
------------ | ------------- | 
lastUpdated | UTC  | 
permissionSetName | String  | 
empNum | Integer  |
empHrId  | Integer | 

assignedSchedules definition:
------------ | ------------- | 
hsId | Integer | 
name | String  | 


**Example Response**

````
[
 {
    "lastUpdated": "2015-07-10T17:39:52.937-05:00",
    "accountCreated": "2012-12-28T13:38:41.677-06:00",
    "permissionSetName": "Employee",
    "empNum": 4003,
    "assignedSchedules": [
      {
        "hsId": 781691496,
        "name": "Bartender",
        "extId": 0
      },
      {
        "hsId": 781691492,
        "name": "Server",
        "extId": 0
      }
    ],
    "empHrId": -1
  }
]
````



```
curl -X GET -H "Content-Type:application/json" -u username:password
 "https://api.bodhi.space/namespace/controllers/vertx/
 hotschedules/1/1/getEmpInfo?active_only=true"
````


## Add employees to a Store

**Method Name:** setEmps


### Request


````
https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules
/1/1/setEmps?
start_day=DD&
start_month=MM&
start_year=YYYY&
end_day=DD&
end_month=MM&
end_year=YYYY&
[{employee}]
````



Property | Primitive | 
------------ | ------------- | 
start_day | Integer  | 
start_year | Integer | 
end_day | Integer | 
end_month | Integer | 
end_year | Integer | 

Array of Employee objects

Property | Primitive | 
------------ | ------------- | 
zipCode | Integer  | 
address | String | 
clientId | Integer  | 
address2 | String | 
city | String  | 
NName | String | 
altId | Integer  | 
empNum | Integer | 
phone | String  | 
dob | UTC | 
state | String  | 
email | String | 
status | Integer | 

**Example Employee object**

````
  {
    "zipCode": "",
    "hireDate": "2016-08-24T10:02:38.770-05:00",
    "address": "",
    "clientId": 14935377,
    "LName": "Perkins",
    "address2": "",
    "city": "",
    "mobile": "",
    "NName": "",
    "altId": -1,
    "FName": "Norbert",
    "empNum": -1,
    "phone": "6502222222",
    "hsId": 1656878857,
    "dob": "1974-12-31T00:00:00-06:00",
    "state": "",
    "storeNum": 2,
    "email": "norbert.perkins@tiffles.com",
    "status": 1
  }
````







````
curl -X PUT -H "Content-Type:application/json" 
-u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules
/1/1/setEmpJobs?
start_day=30&
start_month=4&
start_year=2016&
end_day=5&
end_month=5&
end_year=2016" 
-d "[  {
    "zipCode": "",
    "hireDate": "2016-08-24T10:02:38.770-05:00",
    "address": "",
    "clientId": 14935377,
    "LName": "Perkins",
    "address2": "",
    "city": "",
    "mobile": "",
    "NName": "",
    "altId": -1,
    "FName": "Norbert",
    "empNum": -1,
    "phone": "6502222222",
    "hsId": 1656878857,
    "dob": "1974-12-31T00:00:00-06:00",
    "state": "",
    "storeNum": 2,
    "email": "norbert.perkins@tiffles.com",
    "status": 1
  }]"





## Assign jobs to employees in a store

**Method Name:** setEmpJobs

This method takes in a concept ID, store ID and an array of

### Request


````
/concept/store/setEmpJobs?
start_day=DD&
start_month=MM&
start_year=YYY&
end_day=DD&
end_month=MM&
end_year=YYYY"& 
[{employee_job}, {employee_job}, {employee_job}...]
````


Property | Primitive | 
------------ | ------------- | 
start_day | Integer  | 
start_year | Integer | 
end_day | Integer | 
end_month | Integer | 
end_year | Integer | 
employee | Array | 

Employee Job definition

Property | Primitive | 
------------ | ------------- | 
hsJobId | Integer  | 
regWage | Real | 
posEmpId | Integer | 
hsEmpId | Integer | 
storeNum | Integer | 
ovtWage | Real | 
posJobId | Integer | 
primary | Boolean | 

**Example Employee Job**

````
[
  {
    "hsJobId": 8965542,
    "clientId": 14935377,
    "regWage": 8.8,
    "posEmpId": 4001,
    "hsEmpId": 4177257,
    "storeNum": 2,
    "ovtWage": 13.200001,
    "posJobId": 18,
    "primary": false
  }
]
````




````
curl -X PUT -H "Content-Type:application/json" -u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules
/1/1/setEmpJobs?start_day=30&start_month=4&start_year=2016&
end_day=5&end_month=5&end_year=2016" 
-d "[
  {
    "hsJobId": 8965542,
    "clientId": 14935377,
    "regWage": 8.8,
    "posEmpId": 4001,
    "hsEmpId": 4177257,
    "storeNum": 2,
    "ovtWage": 13.200001,
    "posJobId": 18,
    "primary": false
  }
]"




