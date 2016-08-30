
# Create and run Microservices

Microservices enables large applications to be defined as a suite of modular services. Each module supports a specific business goal and uses a simple, well-defined interface to communicate with other modules.

In this workshop we will look at creating our own microservice and running it in the cloud.

To cater for the different ways in which you want to call and execute a script there are two different engines that run your code that are accessed via two different endpoints.



jsrunner - jvm - asynchronous code, fire and forget (get a task ID)
taskmaster - node.js - fire, runs sync and returns a reponse



Now call your script

````
curl -X POST -H "Content-Type:application/json" -u u:p 
"https://api.bodhi.space/<namespace>/controllers/vertx/taskcontroller/
task?global=false" 
-d '{"name":"getSalesTotals", "type":"application/json", 
"content":{"name":"2016-07-11"}}'
````






For errors or feedback with any of these workshops please contact support@hotschedules.com






