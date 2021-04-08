# REST API

AtroCore is an API-centric application, so a frontend uses REST API to connect with a backend. 
All operations you perform using UI can be used via API calls using the programing language of your choice. 
You can learn how API works if you trace what's going in the network tab in your **browser console** (press F12 key to open the console).

Most of API functions return JSON. POST and PUT requests usually need some data passed in the payload in JSON format.

Requests needs to have the header: `Content-Type: application/json`.

The path to the API in AtroCore is: `api/v1/`. 

Example of GET API request: 

```
GET https://address_of_your_atrocore/api/v1/Product/2d643ca0gff7rh7c6
```

In this documentation we omit the site URL and `api/v1/` path when we show examples of API functions. If you utilize any our client implementation, it will prepend these parts automatically.

> It's recommended to create a **separate API user** with specific rights (roles) and use this user for API calls.

## Authentication

### 1. Obtain an access token

For obtaining access token you need to send GET request to ```/api/v1/App/user``` using [Basic Authentication](http://en.wikipedia.org/wiki/Basic_access_authentication). Username and password should passed through `Authorization` header encoded in base64.

Example:
```
    GET | http://atropim.local/api/v1/App/user
HEADERS | Authorization: Basic " + base64Encode(username + ':' + password)
```
In a response you will get:

* `token` - access token to use

* `acl` - information about user access

* `preferences` - user preferences

* `user` - user record attributes

* `language` - current language

* `settings` - system settings

* `appParams` - additional parameters

### 2. For all further request

For all further requests you should add the following headers:

```
Espo-Authorization: " + base64Encode(username  + ':' + token)
Espo-Authorization-By-Token: true
```

Example:

```
    GET | http://atropim.local/api/v1/Product
HEADERS | Espo-Authorization: " + base64Encode(username  + ':' + token)
          Espo-Authorization-By-Token: true 
```

## REST API documentation
REST API documentation generated in you project automatically. For reading, please, go to ```/apidocs/index.html```.
