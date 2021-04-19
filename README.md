# Backend Task for Engineering Role

Thank you for showing an interest in joining us as a part of UX Gorilla Tech team. 

Please read this document carefully. We've tried to be as specific as we could, but if you feel something is not clear in the task, feel free to raise a issue on Github and someone from our team should reply ASAP.

As a part of the process, please create a server using Node.JS (You're free to use any framework of your choice). Below is a sample specification for the server.

You'll be implementing a basic authentication server.

## 1. Create an app with Node.JS

 #### The API should support the following
- User Signup
- Users Sign-In
- Allow user to access their own information

A `user` must have the following information:
- username
- password (Please hash the passwords, you may use MD5/SHA-2 etc)
- firstname
- lastname

**Please do not use a database to store the User information, store it in a JSON file stored on the local file system. (No MongoDB, No MySQL, No Postgres, No Elasticsearch, No Sqlite) -- Plain old JSON.**



#### Data Validation

#### Some data validations that should be taken care of
- username
	- can only contain lowercase English alphabets (no numbers and special characters) [example: `uxgorilla` is allowed, `UXGorilla` is not allowed, `UXGorilla1` is not allowed, `UX@Gorilla` is not allowed]
	- it should be of at least 4 characters
- password
	- must contain at least 1 uppercase character
	- must contain at least 1 lowercase character
	- must contain at least 1 number
	- no special characters allowed
	- should be of at least 5 characters
- firstname
	- should only contain English alphabets [A-Z, a-z]
- lastname
	- should only contain English alphabets [A-Z, a-z]


### (Requests / Responses)
#### - POST /signup
- The request body should have `username`, `fname`, `lname` and `pasword`
- The body should be application/json
```
{
  "username": "<username>",
  "password": "<password>",
  "fname": "<first_name>",
  "lname": "<last_name>"
}
```
 On success, this should return with HTTP status code 200
```
{
  "result": true,
  "message": "SignUp success. Please proceed to Signin"
}
```
On failure,  either due to empty body, field constraints or missing fields, please check the provided Postman collection.

#### - POST /signin
- The request body should have `username` and `password`
- The body should be application/json
- On successful login, you have to sign a JWT token with the `username` and `firstname` in the JWT payload.
```
{
    "username": "<username>",
    "password": "<password>"
}
```
 On success, this should return with HTTP status code 200
```
{
    "result": true,
    "jwt": "<jwt_token>",
    "message": "Signin success"
}
```
On failure,  either due to empty body, invalid credentials or missing fields, please check the provided Postman collection.

#### - GET /user/me
- Set the Authorization header equal to JWT token you received after POST /signin

On success, this should return with HTTP status code 200
```
{
    "result": true,
    "data": {
        "fname": "<first_name>",
        "lname": "<last_name>",
        "password": "<hashed_password>" // bad practice, doing it just for the task
    }
}
```
On failure, in case of missing token, it should return with HTTP status code 400
```
{
    "result": false,
    "error": "Please provide a JWT token"
}
```
On failure, in case of bad token, it should return with HTTP status code 400
```
{
    "result": false,
    "error": "JWT Verification Failed"
}
```

## 2. Testing your server

You will need to [Download Postman](https://www.postman.com/downloads/) to test your server.

Your code will be evaluated against a postman collection which you can [download here](collection.json). 

The postman collection consists of the tests already written for you. You just have to run all the cases against your application and see if they all pass (green ticks).

You will have to set a few variable names in the Postman collection to run the test cases effectively. ([Here is a video to help understand Postman variables better](https://www.youtube.com/watch?v=ENNsL-XGLus)) 

The collection also defines some variables.
1. `baseUrl` - Set this to the URL of your Express server. IMPORTANT
2. `accessToken` - On SignIn success, this variable is set to the received JWT token
3. `username` - You can put in your username here
4. `password` - You can put in your password here
5. `fname` - You can put in your firstname here
6. `lname` - You can put in your lastname here

For your reference, we have a working API already. You can refer to it while building your own API and making sure requests and responses are identical. To test it against our app, please set the `baseUrl` variable to `https://enigmatic-ridge-06779.herokuapp.com`.

To run all the test cases, click on the "Run" button.
![alt text](https://i.imgur.com/R0HgY3l.png)

If all of your testcase passes (against your sever!), you can proceed to deploy your application on Heroku

## 3. Deploy it to Heroku
If all of the test case pass, you have to deploy your Express server on Heroku (free account works!). You may refer this https://devcenter.heroku.com/articles/deploying-nodejs

You can now submit your deployed URL by simply sending it's link to aman@uxgorilla.com and sidheswar.patra@uxgorilla.com