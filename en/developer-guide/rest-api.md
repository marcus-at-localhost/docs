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

### Basic Authentication

For regular users AtroCore uses [Basic Authentication](http://en.wikipedia.org/wiki/Basic_access_authentication). Username and password (or token) are passed through `Authorization` header encoded in base64.

`"Authorization: Basic " + base64Encode(username + ':' + password)`

It's better to use auth token instead of password when you work with API. In this case you will need to provide username and password/token in `Espo-Authorization` header.

`"Espo-Authorization: " + base64Encode(username  + ':' + passwordOrToken)`

1. Obtain an access token by `GET App/user` request with the username and password passed in `Espo-Authorization` header.

2. Use this token instead of password in `Espo-Authorization` header for all further request.

3. If the request returns 401 error that means either username/password is wrong or token is not valid anymore.

**Authentication Token / User Specific Data**

`GET App/user`

Make this request to retrieve an access token.

Returns:

* `token` - access token to use

* `acl` - information about user access

* `preferences` - user preferences

* `user` - user record attributes

* `language` - current language

* `settings` - system settings

* `appParams` - additional parameters
