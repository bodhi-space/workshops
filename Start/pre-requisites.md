# Pre-requisite Software


The HotSchedules IoT Platform API and HotSchedules Application API can be accessed from any script or programming langauge that can make REST calls. 

Most of the examples in these workshops use cURL to access the REST API.

[Using cURL](https://github.com/bodhi-space/workshops/blob/master/Start/pre-requisites.md#using-curl)    
[Using Bodhi CLI](https://github.com/bodhi-space/workshops/blob/master/Start/pre-requisites.md#using-the-platform-cli)    
[Using Java](https://github.com/bodhi-space/workshops/blob/master/Start/pre-requisites.md#using-java)    
[Using C#](https://github.com/bodhi-space/bodhi-dotnet-superagent)    
[Uisng Ruby](https://github.com/bodhi-space/bodhi-slam)    





## Using cURL

cURL is probably the best way of becoming familiar with the platform API and is a great option to use especially if you plan to write shell scripts to work with the platform data. It's cross platform and can be installed from:

<https://curl.haxx.se/download.html>




## Using the Platform CLI

**bodhi-cli** is a command line tool, that allows app developers to quickly work with the cloud API to create and manage data types and work with the data stored in those types.

**Install Node.js**

The bodhi-cli command line tool uses Node.js as a runtime. Install the latest version of Node.js from:

<https://nodejs.org/en/>


**Install the bodhi-cli using node package manager**

To install the bodhi-cli, you can use the node package manager that comes pre-installed with Node.js.
Open a command prompt (select to run as Administrator on Windows) or terminal and enter

````
npm install -g bodhi-cli
````

To call the bodhi command line, just type 'bodhi' at the terminal prompt.
Help can be accessed by typing 'bodhi --help' at the command prompt.

````
bodhi --help
bodhi [options] <command> [args]

//- Project Commands
pwd         |
init        |
set-default |          <env-name>
get-default |

//- Env Commands
new         | create   <env-name>
ls          | list
view        | print    <env-name>
edit        | modify   [env-overloads]
mv          | rename   <from> <to>  [env-overloads]
cp          | clone    <from> <to>  [env-overloads]
rm          | delete   <env-name>

//- Env Details
user        | whoami   [-e <env-name>]
url         | uri      [-e <env-name>]
namespace   |          [-e <env-name>]
whereami    |          [-e <env-name>]

//- Http Options
ping        |          [-e <env-name>] [env-overloads]
login       | authn    [-e <env-name>] [env-overloads]
get         |          [-e <env-name>] [env-overloads] <path> [--out]
count       |          [-e <env-name>] [env-overloads] <path> [--out]
put         |          [-e <env-name>] [env-overloads] <path> [--out]
post        |          [-e <env-name>] [env-overloads] <path> [--out]
patch       |          [-e <env-name>] [env-overloads] <path> [--out]
delete      |          [-e <env-name>] [env-overloads] <path> [--out]
head        |          [-e <env-name>] [env-overloads] <path> [--out]
options     |          [-e <env-name>] [env-overloads] <path> [--out]

--view      { status, headers, location, id, entity, full, debug }
--color
--flat
--status    include the status code


Options:
  -V, --version           Print version number of the tool  
  -e, --environment       The environment to use            
  -s, --uri               The service provider uri          
  -u, --username, --user  The remote username               
  -p, --password          The remote user's password        
  -n, --namespace         The active namespace              
  -a, --agent             The client user agent             
  -D, --data              A data string to supply           
  -F, --file              The file that contains the json   
  -o, --out               Describe the output               
  --view                  Describe the view                 
  --color                 present the view in console colors  [default: false]
  --flat                  provide flat json structure         [default: false]
  --status                include the status                  [default: false]
  -d, --debug             Show debug output                   [default: false]
  -f, --force             Force the command                   [default: false]
  -v, --verbose           more detailed output                [default: false]
 ````
 
To create a default environment and set up your auth details (so you don't have to type with each request) set up a Bodhi project folder using **bodhi init** and set up your **rbc_project.json** file with the environment variables to access your namespace with your credentials. 
The steps are as follows:


````
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
mkdir bodhiapps
cd bodhiapps
bodhi init  bodhiapps
bodhi new baybridge -s api.bodhi.space -n baybridge -u susanjones -p ABCDE
bodhi set-default baybridge

````

Once installed, the bodhi-cli can be accessed by typing 'bodhi' at the command line. Enter **bodhi --help** to get a full list of the CLI features.




## Using Java 

If you are planning to use Java to access the HotSchedules API  you will need to have the latest version of Java installed (at least 1.8) and have maven installed to build the HotSchedules Java SDK. 

**Install or upgrade your Java version to V1.8**

Go to <https://java.com/> to install the latest version of Java.



**Install Maven**

Go to <https://maven.apache.org/guides/getting-started/> to set up maven.


**Download or clone the HotSchedules Java SDK repository**

Go to <https://github.com/bodhi-space/bodhi-java-superagent> to set up the Java SDK.

