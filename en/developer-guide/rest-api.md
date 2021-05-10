# REST API

AtroCore is an API-centric application, so a frontend uses REST API to connect with a backend. 
All operations you perform using UI can be performed via API requests using the programing language of your choice. 
You can learn how API works if you trace what's going in the network tab in your **browser console** (press F12 key to open the console).

Most of API functions return JSON. POST and PUT requests usually need some data passed in the payload in JSON format.

All requests needs to have the header: `Content-Type: application/json`. 

The path to the API in AtroCore is: `/api/v1/`. Only this path can be used for your API requests.

Example of GET API request: 

```
GET https://address_of_your_atrocore/api/v1/Product/2d643ca0gff7rh7c6
```

> It's recommended to create a **separate API user** with specific rights (configure and assign a role to him) and use this user for API calls.

## 1. Step: Authentication

To be able to use AtroCore API you need to go through authentication and obtain access token. 

For obtaining access token you need to send GET request to `/api/v1/App/user` using [Basic Authentication](http://en.wikipedia.org/wiki/Basic_access_authentication). 

Username and password should passed through `Authorization` header encoded in base64.
```
"Authorization: Basic " + base64Encode(username + ':' + password)
```

Example:
```
    GET | http://atropim.local/api/v1/App/user
HEADERS | Content-Type: application/json
          Authorization: Basic YWR1taW46YWRtaW4=
          Authorization-Token-Lifetime: 2
          Authorization-Token-Idletime: 2
```
> **Authorization-Token-Lifetime** and **Authorization-Token-Idletime** are optional parameters. Unit of measure is **hour**. **0** means no expiration. If these parameters are not transmitted, globally configured parameters are used.

In the response you will get:

* `token` - access token to use

* `acl` - information about user access

* `preferences` - user preferences

* `user` - user record attributes

* `language` - current language

* `settings` - system settings

* `appParams` - additional parameters

## 2. Step: Making requests

For all further API requests you should append the following headers to all your requests:

```
"Authorization-Token: " + base64Encode(username  + ':' + token)
```

Here is the example how you can get list of your products:

```
    GET | http://atropim.local/api/v1/Product
HEADERS | Content-Type: application/json
          Authorization-Token: YWRtaW46WVdSMXRhVzQ2WVdSdGFXND0=
```

## REST API documentation
REST API documentation is generated for each project automatically, based on the core and modules you are using. 

To access it please go to `https://address_of_your_atrocore/apidocs/index.html`.
