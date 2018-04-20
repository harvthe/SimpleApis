# Axway API Manager and portal introduction

## Use Case:
##### As an API owner I want to make weather information available in a programmable way.
The marketing department wants to automate their mailings for bank services information. They have noticed that people react different depending on the weather, for example they only save for a rainy day, if it is a rainy day. They require an API which provides them a forecast so they know when to schedule a mailing and they need an API which gives them the current weather. The requirement is for Bangkok at the moment, it might be needed for other cities in the future.

## Solution:
You have found an API at [openweather](https://openweathermap.org/)  since you are expecting more departments to be needing this API and your company policy is to have a “time to hello,world!” less then 10 minutes you want to make a simplified version of the complex API available from the internal developer portal. 

Access to backend API:
```
Your API key = 7369b7d2c2cd0aed3e2cacd6d6686e4 (this key is currently not valid)
```


Reading through the documentation you have found a method for getting the current weather in bangkok


```
http://api.openweathermap.org/data/2.5/weather?id=1609350&APPID=<APIKey>
```

And you have found a method for getting a 5 day forecast in bangkok

```
api.openweathermap.org/data/2.5/forecast?id=1609350&APPID=<APIkey>
```

### Environment
In this practice you will be using the API manager (as the security team or the API provider) and you will be using the developer portal as an API consumer.

```
Login as a API consumer 
<developer portal url>
Login: developer 
Password: developer

Login as a API provider
<API manager url>
Login: apiadmin
Password: xxxxx
Organisation: API development
```
## Task 1, create a manual backend API using API manager
Login to Apimanager 

```
apiadmin and password
```

Add a new Backend API with the <new API> button, select New to create a manual API
![add backend api](https://github.com/harvthe/SimpleApis/blob/master/backend.png)  

#### Creating a Backend API

![create backend api](https://github.com/harvthe/SimpleApis/blob/master/createbackend.jpg)

The steps to do are:

```
•	Give your backend API a name.
•	Put in the basepath http://api.openweathermap.org
•	The resource path is /data
```

Next we will define the 2 methods we are going to offer the company
![backend first method](https://github.com/harvthe/SimpleApis/blob/master/createweather2.JPG)
 
The first method is to get the 5 day forecast

```
•	Put in the name (forecast)
•	Verb = get
•	Path = /2.5/forecast
•	Response: string
Define a parameter 
•	Name = id
•	You can help developers so they know the 16069350 gets the Bangkok information
```

The next method is to get current forecast
![backend second method](https://github.com/harvthe/SimpleApis/blob/master/createweather3.JPG)

The same information as before, but the path is /2.5/weather/, the naming of the method can be current weather (or give it a local name)

```
•	Put in a name (current)
•	Verb = get
•	Path = /2.5/weather
•	Response: string
Define a parameter 
•	Name = id
•	You can help developers so they know the 16069350 gets the Bangkok information
```

Congratulations! You have now setup the backend system, <Save> your backend API and let’s make it available by virtualising the API as a front-end API

 
#### Creating a frontend API
![createfrontend](https://github.com/harvthe/SimpleApis/blob/master/addfrontend.png)

The main menu adds a Frontend API from the API menu, New API from backend API

![frontend_inbound](https://github.com/harvthe/SimpleApis/blob/master/createweather4.JPG)

The first tab shows how your new API will be found, you will need API REST guidelines to make sure this is handled in a structured way, for now we will make the API avaialbe under api.yourcompany.com/weather
We can define the inbound security, for now we will keep it an open API choose
`<pass Through>`

Select how the security for your backend API (outbound) is done
![frontend_outbound](https://github.com/harvthe/SimpleApis/blob/master/createweather5.JPG)


The API Key is provided previously
Press edit to change
 
The API key field name used from weatherunderground is called 

![api_key_authentication](https://github.com/harvthe/SimpleApis/blob/master/createweather6.JPG)
```
-APPID
-Put in the API key
-The backend api is expecting the API key in a query string
```

Go to the API tab, and see how you will make the API available in your company give it a name and tell people a little about it in the summary
![frontend_API](https://github.com/harvthe/SimpleApis/blob/master/createweather7.JPG)
 
Great!! Select Save, the API is now available in the api development organisation!!

Login to the developer portal, and go to the API page.
See if you can find your new API, and select it
Select one of the methods in your API, put in `bangkok` as your city `id`
Use the `Try it out` button.

You will get an error back saying that Bangkok is not an ID!
Try the same with `1609350`
Try the other method and see if you spot the differences.
![frontend_inbound](https://github.com/harvthe/SimpleApis/blob/master/createweather_portal.JPG) 


Copy the Request URL from the portal and paste it into a new collection and request in postman.
Press `send` (if there is no response, try to put the URL in a browser once to load the certificates)
![Postman_weather_nokey](https://github.com/harvthe/SimpleApis/blob/master/postman_weather_nokey.JPG) 
 
## Use case: Add Security
##### As an API owner I want to add security so I can restrict access to my API
Your API is the most used API in the company, random people are even starting to use it to avoid work when the weather is nice. Security has asked you to restrict access and to implement API keys.
Return to the API Manager and select the Frontend API you have created.

Go to the `inbound` tab and select `API key` for inbound security.
the default value for the API key is `KeyId` feel free to change it (use the same naming in the postman test)
Select `OK`
![addSecurity](https://github.com/harvthe/SimpleApis/blob/master/security.JPG) 

The API is now secured, so we can make it available for other organisations in the bank:
From the `Frontend API` list select the API and from the `Managed selected` menu select `publish` to make this API available for other organisations
![Publish](https://github.com/harvthe/SimpleApis/blob/master/publish.png) 
 

Go back to the Portal, refresh the browser, and see if you can get access to the API.
At this point in time, access is only available to registered apps.
There are multiple ways to create Apps, we will explore the self service capabilities of the dev portal

Select the `Applications` tab on the developer portal
`+Create application` for a new application, give it an application name and select the `Weather API`.
Select `Save` Application 

![apps](https://github.com/harvthe/SimpleApis/blob/master/createapp.JPG) 
 
To generate Keys for the application, select the application you just created. 
Select `Edit the application` 

![appskeys](https://github.com/harvthe/SimpleApis/blob/master/createapp2.JPG) 
 
And press `generate keys` 
![appsmakekeys](https://github.com/harvthe/SimpleApis/blob/master/genkey.png) 
 
The developer portal shows the key immediately. (make a copy of the key in your notepad)

Return to the `API` tab, select the Weather API. Select the key from the `API key` dropdown and now test the API again.

Try the same with your Postman client, without a key you will not get a response if you press `send`
(for this demo we haven't defined status codes)

update the Postman request with the same key you used for the demo
![Postman_weather_apikey](https://github.com/harvthe/SimpleApis/blob/master/postman_weather.JPG) 

## Swagger spec
Return to the API portal
From the API tab, select the Weather API and download the Swagger Spec to a folder on the local computer.
Open a new browser tab and go to: http://editor.swagger.io/#/
Select file and import file to import your swagger file in the online editor.
can you find your own comments and information on the requests???

(there is no option to try the API at the moment, since your API gateway is local)

## provide restricted access for Mark from the Marketing department.
#### as a developer from the marketing department I want to use the API so that i can check on the weather for my marketing campaigns
You got an email from Mark saying he has lost accesss to his API, you will need to help him get a key.
To controll and govern APIs we need to use APIManager

Login back to APImanager and select the `Clients` menu.
![clients](https://github.com/harvthe/SimpleApis/blob/master/clients1.JPG) 
 
From the organizations tab, create a new organization  “marketing” give it a random email address and add the new API to the organization.

![clientsOrg](https://github.com/harvthe/SimpleApis/blob/master/createorg.jpg) 
Optional, press “generate code” this will allow people to self register on the portal with the created code.
For now, we will help Mark a little and setup his account for him.

From the application developer tab in the clients menu, create a new user, create any name, but assure you select the marketing organization.
![clients_usr](https://github.com/harvthe/SimpleApis/blob/master/createusr.JPG) 
 
**IMPORTANT:** after you press `Create` scroll down and select `change password`.
 
Select a password and write this down (or use mark/mark)
![clients_pw](https://github.com/harvthe/SimpleApis/blob/master/password.JPG) 
 
Mark can now login from the Develper portal and create his own application 

go to the developer and `sign out` the current user
-`login` as per the user you just created `mark/mark`
- Go the `Application` tab
- Pretend to be mark and `create application`
- choose an `application name` for instance `marks weather app`
- select the `weather api`
- press `save application`

We have the application defined, but there are no Keys jet! 
- select `marks weather app`
- select `edit the application` under the `API Keys` section.
- under the `API keys` section feel free to generate a few keys 

Go back to your Postman application and check if the new key works.

#### As an API owner I want to restrict traffic to my API so that I secure my backend systems from mis-use
Mark has been abusing the API we need to limit his usage.

Go back to the API manager GUI where we govern the usage of our APIs
From the `clients` menu we can find the same application which mark created in the `applications` tab
![quota](https://github.com/harvthe/SimpleApis/blob/master/appquota.JPG) 

Read through the details and see if you find the keys which Mark just created on the developer portal

From the `Quota` tab we will set a very low quota select `override default quota`. 

![quotaset](https://github.com/harvthe/SimpleApis/blob/master/appquota2.JPG) 
Select the weather API
Throttle all methods `2` messages every `1` **Minute**











 
Use case: New Zealand business information
You have been asked to make the New Zealand business number API available as a re-usable API within the Bank. The API is documented in Swagger format on this link

To begin: add “new API” from “backend API” menu, from the API menu.
Select – Import Swagger API
 

From the next menu, upload the swagger file
 
And provide a name for the new backend API.
Press import to start the import process. For details check on how all methods have been imported automatically
Now, we need to virtualise this API by making it available as Fontend API
Select “New API” from the frontend menu. 
Select from existing backend API and search for the New Zealand business numbers API.

 

For inbound authentication select “pass through” 
Provide a resource path according to your standards ”v1/newZealand”
For outbound keep as (we are not going to connect to the backend)
In the API tab, check the API name, and change if desired. Change the version of your API to 1.0
In the API summary note that this is a fake API.
At the API methods, check if all methods have been integrated
Since this is using a HTTPS service, we need to check if the server certificates have been loaded under “trusted certificates”
Select Save.
Check on the developer portal on how this API is documented and how SDKs are now generated for easy integration into your applications!

Challenge for bonus points!
Download the demo Swagger file 








