# Authentication

## Basic Authentication

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