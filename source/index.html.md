---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---
# WELCOME TO WEConnect

# Introduction

Welcome to the WEConnect API!
WeConnect provides a platform that brings businesses and individuals together. This platform creates awareness for businesses and gives the users the ability to write reviews about the businesses they have interacted with.

You can use our API to access to acces different businesses. We get You connected to multiple businesses, their reviews and profiles. Our API also allows You to add a business to the platform too.

Our language of choice here is node and express was used for the routing. You can view code examples in the dark area to the right, and you can switch the programming language oto javascript with the tabs in the top right.

# Development
This application was built with <a href="https://nodejs.org/en/">node</a> and <a href="https://expressjs.com/en/guide/routing.html">express</a> as the router.

# Installation
* Ensure to have nodeJs and postgreSQL installed
* Clone the Repository github.com/ddouglasz/We-connect
* Switch to the directory: `cd WEConnect`
* Install all dependencies `npm install`
* Start the app using `npm start` for development
* Use postman to consume the API

# Authentication

The WEConnect API uses a login criteria (username and password) to log in and provide acces to routes that require authentication and permission(protected routes). The Api is designed to create a session once logged in. This is possible due to the token generated to secure user sign details. upon failure of generating this token, the user is regarded as unauthorized and as such no privileges are granted for the user to acces authenticated/protected routes.

# API requests

## API endpoints and functions

 

Type of request | route(endpoint)       | Description
----------------| ----------| --------------------
POST   |api/v1/auth/signup|create a new user
POST   |api/v1/auth/login|login existing user
POST   |/api/v1/businesses|create a new business
GET    |/api/v1/businesses|get all businesses
DELETE | /api/v1/businesses/:businessId |delete a particular business
GET    |/api/v1/businesses/:businessId| to retrieve a particular business using its businessId
PUT    |/api/v1/business/:businessId  | to update a particular business using its businessId
POST   |/api/v1/business/:businessId/reviews| to post a review for a given business using its businessId
GET    |/api/v1/business/:businessId/reviews| to get reviews of a particular business using its businessId
GET    |/api/v1/businesses?location=keyword| get businesses based on key word (serach query)
GET    |/api/v1/businesses?category=keyword| get businesses based on key word (serach query).

#Users

##sign Up a User

**request**

* Endpoint: Post: `/api/v1/auth/signup`
* Body `(application/json)`


**Response**

* status: `201 created`
* Body `(application/json)`



```javascript
 
request:

{
  "userId": 1,
  "fullname": "pascal pascal",
  "username": "pascal11",
  "password": "passpass",
  "email": "pas@cal.com"
},


```
 
<aside class="notice">
 x-access-token must be generated to access protected routes. This should be included in the header or body.
</aside>

```javascript
response:

{
  "message": "user registered successfully",
  "token": "jhgjjgvghccrt4765r876tyuutuytdy65476lkn_kjbjhbhuyh.ghgcvhgcgchgfcfghfcgfdteMNhkjbkhj.hjVBzgdxgfdsjgfgf574xcgfxgd"
}

```

##sign in a User

**request**

* Endpoint: Post: `/api/v1/auth/signin`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`



```javascript
 
request:

{
  "username": "pascal11",
  "password": "passpass",
},


```
 
<aside class="notice">
 token must be set to access protected routes. This should be included in the header or body(where you have x-access-token to be token).
</aside>

```javascript
response:

{
  "message": "user signed in successfully",
  "token": "jhgjjgvghccrt4765r876tyuutuytdy65476lkn_kjbjhbhuyh.ghgcvhgcgchgfcfghfcgfdteMNhkjbkhj.hjVBzgdxgfdsjgfgf574xcgfxgd"
}

```


# Businesses

## Get All Businesses

**request**

* Endpoint: Get:`/api/v1/businesses`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`



```javascript
response:

"status": "success",
"Businesses":[{
  "id": "1",
  "name": "andela",
  "mage": "andela.jpg",
  "description": "a software development company changing the face of africa",
  "category": "ICT",
  "locatio": "lagos",
  "email": "andela@andela.com",
},
{
  "id": "2",
  "name": "irokotv",
  "image": "oroko.jpg",
  "description": "online and offline entertainment business",
  "category": "entertainment",
  "location": "portharcourt",
  "email": "iroko@iroko.com",
},
{
  "id": "3",
  "name": "farm crowdy",
  "image": "farmcrowdy.jpg",
  "description": "connects farm owners with investors on farm produce to share profits",
  "category": "farming",
  "location": "kaduna",
  "email": "farmcrowdy@farmcrowdy.com",
}
];

```

## Get One Business

**request**

* Endpoint: Get:`/api/v1/business/2`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`


```javascript

response:

"status": "success",
"Business":[{
   "id": "2",
  "name": "irokotv",
  "image": "oroko.jpg",
  "description": "online and offline entertainment business",
  "category": "entertainment",
  "location": "portharcourt",
  "email": "iroko@iroko.com",
},
 ];
```

##Post a new Business

**request**

* Endpoint:Post: `/api/v1/business/`
* Body `(application/json)`


**Response**

* status: `201 created`
* Body `(application/json)`

```javascript

request:

{
   "id": "2",
  "name": "phazecloud.ng",
  "image": "phazecloud.jpg",
  "description": "home automations business",
  "category": "technology/ICT",
  "location": "abuja",
  "email": "phaze@cloud.com",
},

```
 <aside class="notice">
NOTE: to post, token is needed to create an authenticated session  for a user.
</aside>

```javascript

response:

{
"message":"businesses successfully registered"
{
   "id": "2",
  "name": "phazecloud.ng",
  "image": "phazecloud.jpg",
  "description": "home automations business",
  "category": "technology/ICT",
  "location": "abuja",
  "email": "phaze@cloud.com",
  }
}

``` 
##Delete a new Business

**request**

* Endpoint: Delete:`/api/v1/business/2`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`

```javascript

response:

{
   "Message":"Business succesfully deleted"
},

```
 
<aside class="notice">
NOTE: to post, token is needed to create an authenticated session  for a user. specify business id of the business to be deleted in the params. 
</aside>
 

 ##Edit a Business

**request**

* Endpoint: Put: `/api/v1/business/1`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`

```javascript

request:

{
  {"message":"you have successfully updated the business"
   "id": "2",
  "name": "phazecloud.ng",
  "image": "phazecloud.jpg",
  "description": "home automations business",
  "category": "technology/ICT",
  "location": "abuja",
  "email": "phaze@cloud.com",
 }
}

```
 

 
##Get all businesses Using a key word(search query=location)

**request**

* Endpoint:Post: Get:`/api/v1/business?location=abuja`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`

<aside class="notice">
NOTE: to post, token is needed to create an authenticated session  for a user. Enter the search key word you want to to get all businesses with similar key word(in this case, a location) in one of their params.
given that we enter a query string location of "lagos". we are expected to have a response as seen below with all businesses in abuja from the database.
</aside>

```javascript

response:

{
   "id": "2",
  "name": "phazecloud.ng",
  "image": "phazecloud.jpg",
  "description": "home automations business",
  "category": "technology/ICT",
  "location": "abuja",
  "email": "phaze@cloud.com",
},

```
 

  
#Reviews
##Post a new review to a Business

**request**

* Endpoint:Post: `/api/v1/business/reviews/:businessId`
* Body `(application/json)`


**Response**

* status: `201 created`
* Body `(application/json)`

<aside class="notice">
NOTE: to post, token is needed to create an authenticated session  for a user. user has to be signed in to post a review.
</aside>

```javascript

request:


   {
  "id": 4,
   "review": "truly built on excellence",
}

response:

{
"message":"businesses review successfully added"
   {
  "id": 4,
  "reviewedBy": "pascal",
  "review": "truly built on excellence",
}
}
```

## Get All Reviews for a given business

**request**

* Endpoint: Get:`/api/v1/businesses/busunessId/reviews`
* Body `(application/json)`


**Response**

* status: `200 ok`
* Body `(application/json)`



```javascript
response:

"status": "successful",
"Business": "andela nigeria"
 "reviews": [{
  "id": 1,
  "reviewedBy": "clinton",
  "review": "so much verve and gusto!",
},
{
  "id": 2,
  "reviewedBy": "longe",
  "review": "so much zeal",
},
{
  "id": 3,
  "reviewedBy": "seun",
  "review": "great speed of delivery",
},
{
  id: 4,
  "reviewedBy": "pascal",
  "review": "truly built on excellence",
},
]

```

