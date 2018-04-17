Use Case:
The marketing department wants to automate their mailings for bank services information. They have noticed that people react different depending on the weather, for example they only save for a rainy day, if it is a rainy day. They require an API which provides them a forecast so they know when to schedule a mailing and they need an API which gives them the current weather. The requirement is for Bangkok at the moment, it might be needed for other cities in the future.

Solution:
You have found an API at https://openweathermap.org/ since you are expecting more departments to be needing this API and your company policy is to have a “time to hello,world!” less then 10 minutes you want to make a simplified version of the complex API available from the internal developer portal. 

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

Environment
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




