# Webhooks

## What this does

1. Set up a webhook to watch a type for changes


## Environment
Production Namespace: dipock

set up a script called **pushnotification** and a webhook to call it. set up a type called demovoid that we post data to to force the webhook to fire when the transaction has a name of "Bob" associated with it.

Because the webhook posts the instance if the type you are watching in the JSON payload, it is not possible to use webhooks to call the async task runner process (unless there is something I have not been told) - so it is necessary to call the script using JS Runner method.


## Webhook

Webhook set up to POST to endpoint. The webhook was tested perviously against http://requestb.in/1dtw8vm1 and works.



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
    // set up a loop to run this multiple times
    var arr = [1,2];
	// var async = require('async');  - requires not required as async is a system lib
	async.each(arr, function(num, cb){
		console.info('Set up client context');
        var client = options.connection;
        
        var data = {"to":{"type": "BodhiUser", 
        "where": {"username": "admin__dipock"}},
        "payload": {"message":"This just happened"}};
        console.info('create PUSH notification');
        client.post('notifications', data, function(err, data, ctx) {
                       cb(err);
        });
		cb();
	}, function(err){
		if(err){
			done(err);
		}
		else{
		    // ** warning all scripts must have a done
			done(null, 'callAsync task succeeded');
		}
	});
}
````




## Tests



````
curl -X POST -H "Content-Type:application/json" -u admin__dipock:admin__dipock "https://api.bodhi.space/dipock/controllers/vertx/taskcontroller/task" -d '{"name":"pushnotification", "type":"js", "content":{"name":"script"}}'

````






