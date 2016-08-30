# Using Java to access the HotSchedules Application API

  
Before starting - make sure you have read and installed the [Pre-requisite software](https://github.com/bodhi-space/workshops/blob/master/Start/pre-requisites.md#using-java) to use the Java SDK. This workshop assumes you have successfully compiled the Bodhi Java driver using maven as described in the Java SDK set up instructions. 

Note: it is not necessary to use the Java SDK - but the SDK does simplify and minimise a lot of the additional code you would normally write when accessing a REST service. 


## JAR Files

All the code samples shown in this workshop use the following JAR files. If you plan to copy and run the code samples, please make sure that the following JAR files are included in your build path. 

1. bodhi-java-superagent-0.0.1.jar
2. hamcrest-core-1.3.jar
3. httpasyncclient-4.0.2.jar
4. httpclient-4.5.2.jar
5. httpcore-4.4.5.jar
6. httpcore-nio-4.4.5.jar
7. junit-4.11.jar
8. junit-toolbox-2.3-SNAPSHOT.jar
9. org-apache-commons-logging.jar
10. org.json.jar
11. unirest-java-1.4.9.jar




## Set up the client 

We will configure the Client class with our account details and then use the client in out application tests. We will use Junit tests to test several service methods, just enough for you to get a good understanding of the API calls using the Java driver. 

We will create a new instance of the Client class and set the URL and Namespace properties and the auth credentials. 


For this example, lets assume we have an account called 'tiffles' with a user called 'NorbertPerkins' and a password of 'London'.

````
client =  new Client("https://api.bodhi.space", "tiffles", new BasicCredentials("NorbertPerkins", "London"));
````

**Looking at the complete example**


```
package com.dipock.hsapi;
import com.bodhi.superagent.BasicCredentials;
import com.bodhi.superagent.Client;
import com.googlecode.junittoolbox.PollingWait;
import org.junit.After;
import org.junit.Before;
import java.util.concurrent.TimeUnit;
public class SimpleClient {
	   protected Client client;
	    protected PollingWait wait = new PollingWait().timeoutAfter(50, TimeUnit.SECONDS)
	            .pollEvery(100, TimeUnit.MILLISECONDS);
	    @Before
	    public void init() {
	        client =  new Client("https://api.bodhi.space", "tiffles", new BasicCredentials("NorbertPerkins", "London"));
	    }
	    @After
	    public void clean() {
	        client = null;
	    }
}
```


 

## Calling the HS Platform IoT API

With the client set up we can start to use the API.

This example calls the HS Platform API to return the name and unique identifier for a list of stores.


````
package com.dipock.hsapi;

import java.io.IOException;
import com.bodhi.superagent.Result;
import com.bodhi.superagent.patch.Patch;
import com.bodhi.superagent.patch.PatchOperation;
import com.mashape.unirest.http.JsonNode;
import org.apache.http.HttpStatus;
import org.json.JSONArray;
import org.json.JSONObject;
import org.json.JSONException;
import org.junit.Assert;
import org.junit.Test;

@SuppressWarnings("unused")
public class SimpleTest extends SimpleClient {

	   @Test
	    public void testGetStores() throws JSONException {
	    
	        System.out.println("Test to Get Store data");
	        
	        final Result<JsonNode>[] done = TestUtil.createResultArray(1);
	        client.get("resources/Store?fields=name,display_name,sys_id", null, result -> done[0] = result);
	        wait.until(() -> done[0] != null);
	        Result<JsonNode> result = done[0];
	        
	       Assert.assertEquals(HttpStatus.SC_OK, result.getStatusCode());
	        JSONArray res = result.getData().getArray();
	        Assert.assertNotNull(res);
	        Assert.assertTrue(res.length() > 0);
	        
            System.out.println("Status code: " + result.getStatusCode());
            System.out.println("Store count: " + result.getData().getArray().length());
            
            System.out.println(res);
            
            for (int i=0;i<result.getData().getArray().length();i++) {
            
            	JSONObject object = res.getJSONObject(i);
            	String name = object.getString("name");
            	System.out.println("Store: " + name);
            	// System.out.println( res.get(i).toString()  );            	
            }  
	    }
}

````

## Calling GetEmpInfo method of the HS Application Employee Service



```
	   @Test
	    public void testGetEmpInfo() throws JSONException {
	        System.out.println("test Get Emp Info");
	        
	        final Result<JsonNode>[] done = TestUtil.createResultArray(1);
	        String concept = "1";
	        String storeid = "2";
	        String active = "true";
	        
	        // Call : client.get("controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true", 
	        //                    null, result -> done[0] = result);
	        
	        String url = "controllers/vertx/hotschedules/" + 
	                      concept + "/" + 
	                      storeid + 
	                     "/getEmpInfo?active_only=" + active;
	        
	        client.get(url, null, result -> done[0] = result);
	        wait.until(() -> done[0] != null);
	        Result<JsonNode> result = done[0];
	        
	       Assert.assertEquals(HttpStatus.SC_OK, result.getStatusCode());
	        JSONArray res = result.getData().getArray();
	        Assert.assertNotNull(res);
	        Assert.assertTrue(res.length() > 0);
	        
           System.out.println("Status code: " + result.getStatusCode());
           System.out.println("Employee count: " + result.getData().getArray().length());
           
           System.out.println(res);
           
           for (int i=0;i<result.getData().getArray().length();i++) {
           
           	// JSONObject object = res.getJSONObject(i);
           	System.out.println( res.get(i).toString()  );            	
           }
           
	    }
```



## Calling GetSchedule method of the HS Application Schedule Service


```
	   @Test
	    public void testGetSchedule() throws JSONException {
	        System.out.println("test Get Schedule");
	        
	        final Result<JsonNode>[] done = TestUtil.createResultArray(1);
	        
	        String concept = "1";
	        String storeid = "2";
	        String sdd = "1";
	        String smm = "2";
	        String syy = "2016";
	        String edd = "1";
	        String emm = "3";
	        String eyy = "2016";	        	        
	        
	        // client.get("controllers/vertx/hotschedules/1/2/getScheduleV3?
	        //             start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016",
	        //             null, result -> done[0] = result);
	        
	        String url = "controllers/vertx/hotschedules/" + concept + "/" + storeid + 
	                     "/getScheduleV3?start_day=" + sdd + 
	                     "&start_month=" + smm + 
	                     "&start_year=" + syy + 
	                     "&end_day=" + edd +
	                     "&end_month=" + emm +
	                     "&end_year=" + eyy;
	                     
	        client.get(url,null, result -> done[0] = result);
	        wait.until(() -> done[0] != null);
	        Result<JsonNode> result = done[0];
	        
	       Assert.assertEquals(HttpStatus.SC_OK, result.getStatusCode());
	        JSONArray res = result.getData().getArray();
	        Assert.assertNotNull(res);
	        Assert.assertTrue(res.length() > 0);
	        
          System.out.println("Status code: " + result.getStatusCode());
          System.out.println("Schedule count: " + result.getData().getArray().length());
          
          for (int i=0;i<result.getData().getArray().length();i++) {
          
          	// JSONObject object = res.getJSONObject(i);
 
          	System.out.println( res.get(i).toString()  );            	
          }
          
	  }   
```


