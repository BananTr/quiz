# quiz

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

# Api info
## Endpoint for login 

*The request Uri:*
https://v2202107122785158474.goodsrv.de/api/rest-auth/login/

*The request method: Post*

*The request body:*
```json
{
 "email": "test@test.com",
 "password": "testtest"
}
```

The response:
```json
{
 "key": "dfds4345rdfgdfgertret..."
}
```
-----
## Endpoint for get user 

*The request Uri:*
https://v2202107122785158474.goodsrv.de/api/rest-auth/user/

*The request method:* Get

*The request Header:*
```json
{
 "headers":{"Authorization": "Token ${key}"}
}


```

The response:
```json
{
    "pk": 5,
    "username": "Test",
    "email": "test@test.com",
    "is_staff": false
}


```
