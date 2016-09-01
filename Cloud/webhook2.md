## Webhook

Webhook set up to POST to endpoint. The webhook was tested perviously against http://requestb.in/1dtw8vm1 and works.

# Lab 2: Call a script

set up a script called **pushnotification** and a webhook to call it. set up a type called demovoid that we post data to to force the webhook to fire when the transaction has a name of "Bob" associated with it.



## What this lab does

1. Set up a webhook to watch a data type for changes
2. Post a message to an endpoint.
3. Send an in-app push notification to your device


## Pre-requisites



https://api.bodhi.space/dipock/controllers/vertx/scripts/pushnotification


````

verify: false
type:  "DemoVoid"
retries: 5
url: "https://api.bodhi.space/dipock/controllers/vertx/scripts/pushnotification"
event: [0]:  "i"
description: "watches a type then calls a script that pushes a notification"
fail_count: 0
name:  "CLONE - call-push-script"
match_expressions: Array [1]
 0: Object
property:  "name"
op:  "$eq"
val:  "Bob"
authorization: "BCtHJOPT11gqfiefpd6IlXcGkq4t5DMgYOCicLawFx9WDvBPcZP92M8E0LD7Ynxj3edR"
status:  "Active"
sys_id:  "579a84b54f8621196d2ce749"

````



## Script

Name: pushnotification
Main: main
Source:

````
exports.main = function (options, done){
    console.log('DAS: This script uses async');
    var arr = [1,2,3];
	var async = require('async');
	async.each(arr, function(num, cb){
		console.log('DAS: Set up client context');
        var client = options.connection;
        var data = {"to":{"type": "BodhiUser", "where": {"username": "admin__dipock"}},"payload": {"message":"ASYNC: This just happened"}};
        console.log('DAS: create PUSH notification');
        client.post('notifications', data, function(err, data, ctx) {
                       cb(err);
        });
     
		cb();
	}, function(err){
		if(err){
			done(err);
		}
		else{
			done(null, 'DAS: callAsync task succeeded');
		}
	});
}
````




## Tests



````
curl -X POST -H "Content-Type:application/json" -u admin__dipock:admin__dipock "https://api.bodhi.space/dipock/controllers/vertx/taskcontroller/task" -d '{"name":"pushnotification", "type":"js", "content":{"name":"script"}}'

````






