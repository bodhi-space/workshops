# Sending emails





## Using the Email Template


Step1 Edit the src.html file.  
Step2 Edit the src.txt file.  
Step3 Edit the src.meta.json file.  
Run grunt build  

Your completed email is available in dist/dist.json  

Step4 POST the template to the server.

From the directory the json file is, insert into BodhiEmailTemplate using the following command:  

````
curl -X POST -u admin__base:<password> -H "Content-Type: application/json" --data @template.json <host>/namespace/resources/BodhiEmailTemplate
````




````
curl -X POST -H "Content-Type:application/json" -u admin__dipock:admin__dipock "https://api.bodhi.space/dipock/emails/INVITATION_SELFSIGNUP" -d '{"email":"dipockdas@gmail.com"}'
````




Framework for Email html and css
http://zurb.com/ink/docs.php

Once you have the template in place, the email is saved in the API as a document in the BodhiEmailTemplate type with the following properties

name => A unique name for your template that will be references in the api endpoint you used to send the email
description 
from = > originating email, currently  “The HotSchedules IoT Platform (Formerly Known As Bodhi) Customer Support <bodhi.customer@gmail.com>"
subject => the subject line of your email
language => ‘en_us’
body_txt => the plain text content of your email
body_html => the inlined and minified html of your email

you can see the base templates at 
<host>/<namespace>/resources/BodhiEmailTemplate

There are instructions on how to do the inlining and compressing manually in the read me here
https://bitbucket.org/redbookplatform/email-template-forgot-pw

but I configured these as grunt tasks in this blank template here, which i would recommend as your starting place
https://bitbucket.org/redbookplatform/email-template-blank/overview

Emails use handlebars templates http://handlebarsjs.com/expressions.html
which provide powerful templating

there are some standard template variables accessible to all emails

{{bodhi_host}} => the platform env, bodhi-dev.io or bodhi.space or bodhi-qa.io or whatever
{{namespace}} => the namespace the email is sent in
there might be others

you can also set custom variables which you can set when you make the request to send your email

ENDPOINTS FOR EMAILS
sending emails can be triggered by  POST requests to two endpoints, depending on whether or not you have access to the username or the email address of the user

POST => /emails/<templateName>
template name is the “name” you set when you created the email
using this endpoint you need to include the email address in the body of your post request
{
“email”: “whatever@whatever.com”,
“custom_var” : “something”,
“custom_var2”:”somethingelse
}

you can access these custom_vars as handlebars expressions in your template.

POST => /emails/<templateName>/<username>
{
	“custom_var”:”something”
}

using this endpoint will send an email to the email address associated with the user… but if there isn’t an email address you may get an error. using this endpoint will give you access to a {{username}} variable.

Some additional notes:
Use instructions on how to download blank email template:
https://bitbucket.org/redbookplatform/email-template-count-installed
https://bitbucket.org/redbookplatform/email-template-reveal-installed

To modify the templates:
clear src.html file and paste the current html file
Edit the src.txt file based on text in src.html
Edit the src.meta.json file.
Run grunt build twice

dist.html should be updated after grunt build
dist.html should be updated after grunt build
dist.txt  should be updated after grunt build

copy whole dist.json file
create any test namespace 

POST the template to the server in BodhiEmailTemplate

how to send template?
use emails type:
post the template name to the templatename field (u can get the names by GET from BodhiEmailTemplate type)
in the body provide email in json format, also provide all the variable we use inside the html/txt file like “admin”:”olia”, “domain”:"https://apps”,
If everything works - update all branches with new templates and make pull request


```` 
curl -X POST -u admin__dipock:admin__dipock -H "Content-Type: application/json" --data @./dist/dist.json https://api.bodhi.space/dipock/resources/BodhiEmailTemplate
````



