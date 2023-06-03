---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - python

toc_footers:
#  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
#  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Polypharm mobile API
---

# Introduction

Welcome to PolypharmSolutions Mobile API Documentations. API is intended for use in PolypharmSolutions mobile application.
The API is work in progress.

You can use or add a test user with necessary fields already added. Look for Add Test User in the docs.

This API documentation page was created with [Slate](https://github.com/slatedocs/slate).

# Authentication

API uses user keys to enable authentication. Routes are only valid when used with an authorization header.
Provide authorization header for each API request. The authorization key is recieved by logging in.

`Authorization: kg94385kgdsfj`

<aside class="notice">
You must replace <code>kg94385kgdsfj</code> with your personal API key.
</aside>

## Register

Takes a user model, saves it to database and sends a registration confirmation mail.

### HTTP Request

```python
response = requests.post('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/auth/register', json=user)
```


`POST https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/auth/register`

### Request Body

Takes in a JSON with user object. 

> Example user

```json
{
  "user": {
    "email": "email@email.com",
    "password": "password123"
  }
}
```

### Body

{
  "user": user
}

fields | type         | description
------ |--------------| -----------
"user" | user         | See below for description


### user

fields | type | description
------ | ---- | -----------
email | string | /
password | string | /

### Response
Code | Meaning
---------- | -------
200| Success -- Registration successful
403| Error -- User already exists




## Login

Produces an authorization token, used for accessing routes.

### HTTP Request

```python
response = requests.post('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/auth/login', json=login_data)
```


`POST https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/auth/login`

### Body

> Example body

````json
{
   "email": "email@email.com",
   "password": "password123"
}
````

fields | type | description
------ | ---- | -----------
email | string | /
password | string | /

### Returns

> The POST returns response body

````json
{
   "Authorization": "kg94385kgdsfj",
}
````

{"Authorization":  "kg94385kgdsfj"}

fields | type            | description
------ |-----------------| -----------
Authorization | string          | An authorization token used for verifying users


### Response

Code | Meaning
---------- | -------
200| Success -- Login successful
404| Error -- User not found
404| Error -- Password incorrect

# User
User related operations

## Me
Returns user profile

<aside class="notice">
Requires an authorization header.
</aside>

### HTTP Request

>Set Authorization headers

````json
{
  "Authorization": "kg94385kgdsfj"
}
````

>Example code

```python
headers = {'Authorization': "kg94385kgdsfj"}
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/me', headers=header)
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/me`

### Returns

> The POST returns response body

````json
{
  "userModel": {
    "createdOn": "2023-04-16T15:07:40.010492",
    "email": "example@mail.com",
    "id": 3,
    "passwordHash": "$6$rounds=656"},
  "userDetails": {
    "weight": 85,
    "firstName": "Ivan",
    "condition": ["Alcholism", "Something else"],
    "birthYear": 1952,
    "lastName": "Horvat",
    "userDiscovery": "Facebook",
    "id": 1,
    "height": 175,
   "sex": "male"
  }
}
````

{
  "userModel": userModel,
  "userDetails": userDetails
}

fields | type        | description
------ |-------------| -----------
"userModel" | userModel   | See below for description
"userDetails" | userDetails | See below for description


### userModel

fields | type | description
------ | ---- | -----------
email | string | /
passwordHash | string | /
id | integer | /
created_on | datetime |

### userDetails

fields | type            | description
------ |-----------------| -----------
firstName | string          |
lastName | string          | /                                   
birthYear | integer         | year as integer                               
sex | "male" OR "female" | /                                             
height | integer         | in cm                                         
weight | integer         | in kg                                         
condition | [string, string] | list of strings                               
userDiscovery |  string         | where did user hear about us, simple dropdown

### Response
Code | Meaning
---------- | -------
200| Success 
403| Error -- Invalid access token

## Update User Details
Changes user details such as height, weight and others.
<aside class="notice">
Requires an authorization header.
</aside>

### HTTP Request

>Example code

```python
headers = {'Authorization': "kg94385kgdsfj"}
body = {
  'userDetails': {
    "firstName": "Ivan",
    "lastName": "Horvat",
    "birthYear": 1978,
    "sex": "male",
    "height": 193,
    "weight": 105,
    "condition": ["Alcoholism", "Headache", "Hypertension"],
    "userDiscovery": "Doctor"
    }
}
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/update_user_details', headers=header, body=body)
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/update_user_details`

### Request Body

Takes in a JSON with userDetails object. 

> Example userDetails object

```json
{
  "userDetails": {
    "firstName": "Ivan",
    "lastName": "Horvat",
    "birthYear": 1978,
    "sex": "male",
    "height": 193,
    "weight": 105,
    "condition": ["Alcoholism", "Headache", "Hypertension"],
    "userDiscovery": "Doctor"
  }
}
```

### Body

{
  "userDetails": userDetails
}

fields | type         | description
------ |--------------| -----------
"userDetails" | userDetails  | See below for description

### userDetails

fields | type            | description
------ |-----------------| -----------
firstName | string          |
lastName | string          | /                                   
birthYear | integer         | year as integer                               
sex | "male" OR "female" | /                                             
height | integer         | in cm                                         
weight | integer         | in kg                                         
condition | [string, string] | list of strings                               
userDiscovery |  string         | where did user hear about us, simple dropdown

<aside class="warning">
List of available conditions is generated by calling the API for getting the conditions
</aside>

### Response
Code | Meaning
---------- | -------
200| Success -- User details updated successfully
404| Error -- User not found
403| Error -- Invalid access token

## Update Condition
Changes user condition. For example if user gets over a condition or has a new one.
<aside class="notice">
Requires an authorization header.
</aside>
<aside class="warning">
List of available conditions is generated by calling the API for getting the conditions
</aside>

### HTTP Request

>Example code

```python
headers = {'Authorization': "kg94385kgdsfj"}
body = {'conditions': ['Headache', 'Stomach pain']}
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/conditions', headers=header, body=body)
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/conditions`

### Request Body

Takes in a JSON with user object. 

> Example user

```json
{
  "user": {
    "email": "email@email.com",
    "password": "password123"
  },
  "userDetails": {
    "firstName": "Ivan",
    "lastName": "Horvat",
    "birthYear": 1978,
    "sex": "male",
    "height": 193,
    "weight": 105,
    "condition": ["Alcoholism", "Headache", "Hypertension"],
    "userDiscovery": "Doctor"
  }
}
```

### Body

{
  "user": user,
  "userDetails": userDetails
}

fields | type         | description
------ |--------------| -----------
"userDetails" | userDetails  | See below for description


### userDetails

fields | type            | description
------ |-----------------| -----------
firstName | string          |
lastName | string          | /                                   
birthYear | integer         | year as integer                               
sex | "male" OR "female" | /                                             
height | integer         | in cm                                         
weight | integer         | in kg                                         
condition | [string, string] | list of strings                               
userDiscovery |  string         | where did user hear about us, simple dropdown

<aside class="warning">
List of available conditions is generated by calling the API for getting the conditions
</aside>

### Response
Code | Meaning
---------- | -------
200| Success -- Conditions updated successfully
400| Error -- Conditions field is required
403| Error -- Invalid access token

## Add Therapy

>Example code

```python
headers = {'Authorization': "kg94385kgdsfj"}
therapy = {
    "drugId": 1691,
    "productId": 2554,
    "dose": 800,
    "unit": 'mg',
    "quantity": 3,
    "frequency": 'daily',
    "duration": 10,
    "treats": 'Headache',
    "startDate": str(datetime.now()),
    "endDate": str(datetime.now()),
    "timeOfDay": str(time(14, 30)),
}
requests.post('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/add_therapy', json=therapy, headers=headers).json()
```

Adds a medication to users therapy history.
<aside class="notice">
Requires an authorization header.
</aside>

### HTTP Request

`POST https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/add_therapy`

### Request Body

>Example body

````json
{
    "drugId": 1691,
    "productId": 2554,
    "dose": 800,
    "unit": "mg",
    "quantity": 3,
    "frequency": "daily",
    "duration": 10,
    "treats": "Headache",
    "startDate": "2023-04-16",
    "endDate": "2023-04-16",
    "timeOfDay": "14:30:00"
}   
````
### UserTherapy object
{
    "drugId": int,
    "productId": int,
    "dose": float,
    "unit": string,
    "quantity": float,
    "frequency": string,
    "duration": int,
    "treats": string,
    "startDate": DateTime string,
    "endDate": DateTime string,
    "timeOfDay": Time string
}

fields | type        | description
------ |-------------| -----------
"drugId" | int         | Ingredient ID
"productId" | int         | Product ID
"dose" | float       | How strong is the medicine, e.g. 30mg
"unit" | string      | How is it measured
"quantity" | int         | How many to take each time
"frequency" | string      | How often to take
"duration" | int         | How many days is the therapy
"treats" | string      | What is it for
"startDate" | Date string | /
"endDate" | Date string | /
"timeOfDay" | Time string | When to take

### Returns
Returns added UserTherapy object

> Returns added UserTherapy object

````json
 {
    "dose": 800.0,
    "quantity": 3.0,
    "productId": 884,
    "treats": "Headache",
    "frequency": "daily",
    "startDate": "2023-04-17",
    "createdOn": "2023-04-17",
    "endDate": "2023-04-17",
    "isCompleted": 0,
    "duration": 10,
    "unit": "mg",
    "timeOfDay": "14:30:00",
    "id": 2,
    "drugId": 363
 }
````
### Response

Code | Meaning
---------- | -------
200| Success -- Therapy added successfully
403| Error -- Invalid access token

## Active Therapies
Get all active therapies
<aside class="notice">
Requires an authorization header.
</aside>

>Example code

```python
requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/active_therapies', headers=headers).json()
```

### HTTP Request

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/active_therapies`

### Returns

> GET returns response body

````json
[
  {
    "dose": 800.0,
    "quantity": 3.0,
    "productId": 2554,
    "treats": "Headache",
    "frequency": "daily",
    "startDate": "2023-04-16T23:38:27.363363",
    "createdOn": "2023-04-16T23:38:25.281431",
    "endDate": "2023-04-16T23:38:27.363380",
    "isCompleted": 0,
    "duration": 10,
    "unit": "mg",
    "timeOfDay": "14:30:00",
    "id": 1,
    "drugId": 1691
  },
 {
    "dose": 800.0,
    "quantity": 3.0,
    "productId": 884,
    "treats": "Headache",
    "frequency": "daily",
    "startDate": "2023-04-17T10:01:02.249621",
    "createdOn": "2023-04-17T09:25:25.711994",
    "endDate": "2023-04-17T10:01:02.249639",
    "isCompleted": 0,
    "duration": 10,
    "unit": "mg",
    "timeOfDay": "14:30:00",
    "id": 2,
    "drugId": 363
 }
]
````

[
  {UserTherapy},
  {UserTherapy}
]

fields | type                        | description
------ |-----------------------------| -----------
/   | list of UserTherapy objects | 

### UserTherapy object

fields | type            | description
------ |-----------------| -----------
"id" | int             | UserTherapy ID
"drugId" | int             | Ingredient ID
"productId" | int             | Product ID
"dose" | float           | How strong is the medicine, e.g. 30mg
"unit" | string          | How is it measured
"quantity" | int             | How many to take each time
"frequency" | string          | How often to take
"duration" | int             | How many days is the therapy
"treats" | string          | What is it for
"startDate" | DateTime string | /
"endDate" | DateTime string | /
"createdOn" | DateTime string | /
"timeOfDay" | Time string     | When to take
"isCompleted" | int             | Is it finished


### Response
Code | Meaning
---------- | -------
200| Success
403| Error -- Invalid access token


## Complete Therapy
Completes a therapy due to completion or discontinuation.
<aside class="notice">
Requires an authorization header.
</aside>

>Example code

```python
requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/complete_therapy/1', headers=headers)
```

### HTTP Request

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/complete_therapy/<therapy_id>`

### Route parameters
parameter | type | description        
------ |------| -------------------|
therapy_id | int  | ID of the therapy to be completed

### Response
Code | Meaning
---------- | -------
200| Success -- Therapy added successfully
403| Error -- Invalid access token
404| Error -- Therapy not found

## Add Appointment
Adds an appointment to appointment model.
<aside class="notice">
Requires an authorization header.
</aside>

>Example code

```python
appointment = {
    'doctor': 'Mr. Md Doctor',
    'institution': 'Rebro',
    'date': str(datetime.now()),
}
requests.post('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/add_appointment', json=appointment, headers=headers)
```

### HTTP Request

`POST https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/add_appointment`

### Request Body

>Example body

````json
{
    "doctor": "Mr. Md Doctor",
    "institution": "Rebro",
    "date": "2023-04-17 13:45:05.207232"
}   
````

{
    "doctor": "Mr. Md Doctor",
    "institution": "Rebro",
    "date": "2023-04-17 13:45:05.207232"
}

fields | type            | description
------ |-----------------| -----------
"doctor" | string          | Doctor name
"institution" | string          | Institution name
"date" | string          | Datetime timestmap

### Response
Code | Meaning
---------- | -------
200| Success -- Appointment added successfully
403| Error -- Invalid access token

## Active Appointments
Get all active appointments.
<aside class="notice">
Requires an authorization header.
</aside>

>Example code

```python
requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/active_appointments', headers=headers).json()
```

### HTTP Request

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/active_appointments`

### Returns

> GET returns response body

````json
[
  {
    "institution": "Rebro",
    "createdOn": "2023-04-17T13:30:40.141132",
    "doctor": "Mr. Md Doctor",
    "date": "2023-04-17T13:34:26.990152",
    "isCompleted": 0,
    "id": 1
  }
]
````

[
  {UserAppointment},
  {UserAppointment}
]

fields | type                            | description
------ |---------------------------------| -----------
/   | list of UserAppointment objects | 

### UserAppointment object

fields | type            | description
------ |-----------------| -----------
"id" | int             | UserAppointment ID
"date" | DateTime string | Appointment date and time
"createdOn" | DateTime string | /
"doctor" | string          | Name of the doctor
"institution" | string          | Name of the institution
"isCompleted" | int             | Is it finished


### Response
Code | Meaning
---------- | -------
200| Success
403| Error -- Invalid access token

## Complete Appointment
Finishes an appointment as completed or missed.
<aside class="notice">
Requires an authorization header.
</aside>

>Example code

```python
requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/complete_appointment/1', headers=headers)
```

### HTTP Request

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/complete_appointment/<appointment_id>`

### Route parameters
parameter | type | description        
------ |------| -------------------|
appointment_id | int  | ID of the appointment to be completed

### Response
Code | Meaning
---------- | -------
200| Success -- Appointment completed
403| Error -- Invalid access token
404| Error -- Appointment not found

## Daily Wellbeing Rating
Rates the daily wellbeing.
<aside class="notice">
Requires an authorization header.
</aside>

>Example code

```python
requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/rate_wellbeing/5', headers=headers)
```

### HTTP Request

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/rate_wellbeing/<rating>`

### Route parameters

parameter | type | description        
------ |------| -------------------|
rating | int  | Daily wellbeing rating

### Response
Code | Meaning
---------- | -------
200| Success -- Daily wellbeing rated successfully!
403| Error -- Invalid access token

## Add test user
Adds a therapy and appointment fields to the test user. If the user doesn't exist it creates the user.

Test user | Credentials
---------- | -------
email| test@test.com
password| test

>Example code

```python
requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/add_test_user')
```

### HTTP Request

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/user/add_test_user`

### Response
200| Success -- Test user added successfully


# Polypharm
Functionalities that are related to personalized medicine selection and/or evaluation.

## Conditions
Returns a list of all conditions that a user can input.

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/conditions')
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/conditions`

### Returns

> GET returns response body

````json
[
  "Hyponatremia",
  "Hypocalcemica",
  "Xeroderma Pigmentosum"
]
````

[
  "Hyponatremia",
  "Hypocalcemica",
  "Xeroderma Pigmentosum",
  ...
]

### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- PolypharmData API error


## Units
Returns a list of all measurement units that can be used for drugs.

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/units')
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/units`

### Returns

> GET returns response body

````json
[
  "mg",
  "mL",
  "g"
]
````

[
  "mg",
  "mL",
  "g",
  ...
]

### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- PolypharmData API error


## Find drug
Searches a user input string to find a product or an active ingredient

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/find_drug?string=iburpforen')
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/find_drug?string=<param>`

### Query parameters

parameter | type   | description        
------ |--------| -------------------|
"string" | string | Whatever you're looking for

### Returns

> GET returns response body

````json
{
  "Ingredients": [
    {
      "id": 1691, 
      "name": "ibuprofen"
    }
  ],
 "Products": [
   {
     "brand_name": "Ibuprofen Belupo",
     "dose": 800.0,
     "id": 2554,
     "unit": "mg"
   },
  {
    "brand_name": "Dalsy", 
    "dose": 100.0, 
    "id": 2555, 
    "unit": "ml"
  },
  {
    "brand_name": "Ibuprofen Alkaloid",
    "dose": 100.0,
    "id": 2557,
    "unit": "ml"
  },
  {
    "brand_name": "Dalsy forte",
    "dose": 200.0, 
    "id": 2558, 
    "unit": "ml"
  },
  {
    "brand_name": "Ibuprofen JGL",
    "dose": 100.0, 
    "id": 2559, 
    "unit": "ml"
  }]
}
````

{
  "Ingredients": ingredient,
  "Products": product
}

fields | type       | description
------ |------------| -----------
"Ingredients" | ingredient | An active pharmaceutical ingredient
"Products" | product    | A branded pharmaceutical product


### ingredient

fields | type    | description
------ |---------| -----------
id | integer | Primary key of the product
name | string  | /

### product

fields | type    | description
------ |---------| -----------
brand_name | string  |
dose | float   | How strong it is, e.g. 30 mg                                   
id | integer | Primary key of the product
unit | string  | How is it measured, e.g. in mg


### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- You must provide a valid query parameter string
400| Error -- PolypharmData API error


## Ingredient
Returns an ingredient model from an ingredient ID

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/ingredient/1691')
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/ingredient/<id>`

### Route parameters

parameter | type | description        
------ |------| -------------------|
id | int  | ID of the ingredient

### Returns

> GET returns response body

````json
{
  "cyp1a2Inhibition": 0.06,
  "cyp2c19Inhibition": 0.05,
  "cyp2c9Inhibition": 0.2,
  "cyp2d6Inhibition": 0.0,
  "cyp3a4Inhibition": 0.0,
  "drugbankId": "DB01050",
  "id": 1691,
  "ingredient": "ibuprofen",
  "name": "ibuprofen",
  "prevents": ["Pain"],
  "treats": [
    "Arthritis, Juvenile",
    "Arthritis, Rheumatoid",
    "Bursitis",
    "Dysmenorrhea",
    "Fever",
    "Gout",
    "Inflammation",
    "Menorrhagia",
    "Osteoarthritis",
    "Pain, Postoperative",
    "Premenstrual Syndrome",
    "Spondylitis, Ankylosing"
  ]
}
````

{
  "cyp1a2Inhibition": float,
  "cyp2c19Inhibition": float,
  "cyp2c9Inhibition": float,
  "cyp2d6Inhibition": float,
  "cyp3a4Inhibition": float,
  "drugbankId": string,
  "id": int,
  "ingredient": string,
  "name": string,
  "prevents": [string],
  "treats": [string]
}

fields | type             | description
------ |------------------| -----------
"cyp1a2Inhibition" | float            | Inhibition of the CYP1A2 enzyme
"cyp2c19Inhibition" | float            | /
"cyp2c9Inhibition" | float            | /
"cyp2d6Inhibition" | float            | /
"cyp3a4Inhibition" | float            | /
"drugbankId" | string           | ID in the Drugbank database
"id" | string           | Primary key
"ingredient" | string           | /
"name" | string           | /
"prevents" | [string, string] | List of conditions (strings) which medicine can prevent
"treats" | [string, string] | List of conditions (strings) which medicine can treat

### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- You must provide a product ID
400| Error -- PolypharmData API error

## Product
Returns a product model from a product ID

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/product/2554')
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/product/<id>`

### Route parameter

parameter | type | description        
------ |------| -------------------|
id | int  | ID of the product

### Returns

> GET returns response body

````json
{
  "atc": "M01AE01",
  "brand_name": "Ibuprofen Belupo",
  "dose": 800.0,
  "drug_id": 1691,
  "indication": "NaN",
  "local_generic_name": "ibuprofen ",
  "manufacturer": "Belupo",
  "prescribing_level": "NaN",
  "quantity": 30.0,
  "route": "O",
  "unit": "mg"
}
````

{
  "atc": string,
  "brand_name": string,
  "dose": float,
  "drug_id": int,
  "indication": string,
  "local_generic_name": string,
  "manufacturer": string,
  "prescribing_level": string,
  "quantity": float,
  "route": string,
  "unit": string
}

fields | type   | description
------ |--------| -----------
atc | string | /
brand_name | string | /
dose | float  | How strong it is, e.g. 30mg
drug_id | int    | /
indication | string | /
local_generic_name | string | /
manufacturer | string | /
prescribing_level | string | Who can prescribe it
quantity | float  | How many are in a box of the product
route | string | How do you take it
unit | string | What is the unit, e.g. in mg

### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- You must provide a product ID
400| Error -- PolypharmData API error

## Analyze regimen
Analyzes current user's active therapeutic regimen.
<aside class="notice">
Requires an authorization header.
</aside>

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/analyze_regimen', headers=headers)
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/analyze_regimen`

### Returns

> GET returns response body

````json
{
  "contraindications": [
    {"condition": "Drug Hypersensitivity", "drug": 363},
    {"condition": "Hyperaldosteronism", "drug": 363},
    {"condition": "Hypotension", "drug": 363},
    {"condition": "Pregnancy", "drug": 363},
    {"condition": "Asthma", "drug": 1691},
    {"condition": "Drug Hypersensitivity", "drug": 1691},
    {"condition": "Pregnancy Trimester, Third", "drug": 1691},
    {"condition": "Pregnancy, Abdominal", "drug": 1691},
    {"condition": "Rhinitis", "drug": 1691},
    {"condition": "Bronchial Hyperreactivity", "drug": 1691},
    {"condition": "Drug Hypersensitivity", "drug": 3220},
    {"condition": "Lactation", "drug": 3220},
    {"condition": "Liver Diseases", "drug": 3220},
    {"condition": "Pregnancy", "drug": 3220},
    {"condition": "Liver Failure", "drug": 3220}],
  "interactionAde": [
    {
      "condition_concept_name": "Hypertensive emergency",
      "drug_1_id": 363,
      "drug_2_id": 3220,
      "significance": 3.345304142782046
    },
    {
      "condition_concept_name": "Colitis microscopic",
      "drug_1_id": 1691,
      "drug_2_id": 3220,
      "significance": 3.204154230157523},
    {
      "condition_concept_name": "Diabetic neuropathy",
      "drug_1_id": 1691,
      "drug_2_id": 3220,
      "significance": 2.661118035930371
    },
    {
      "condition_concept_name": "Spinal osteoarthritis",
      "drug_1_id": 363,
      "drug_2_id": 1691,
      "significance": 2.550854985988092
    },
    {
      "condition_concept_name": "Neutrophilic dermatosis",
      "drug_1_id": 363,
      "drug_2_id": 3220,
      "significance": 2.549737785988092
    }
  ],
  "interactionCount": 3,
  "interactions": [
    {
      "description": "The metabolism of Atorvastatin can be decreased when combined with Losartan.",
      "drug_1_id": 363,
      "drug_2_id": 3220,
      "id": 842954,
      "source": "Drugbank"
    },
    {
      "description": "The risk or severity of renal failure, hyperkalemia, and hypertension can be increased when Losartan is combined with Ibuprofen.",
      "drug_1_id": 363,
      "drug_2_id": 1691,
      "id": 843044,
      "source": "Drugbank"
    },
    {
      "description": "The metabolism of Atorvastatin can be decreased when combined with Ibuprofen.",
      "drug_1_id": 1691,
      "drug_2_id": 3220,
      "id": 1259755,
      "source": "Drugbank"
    }],
  
  "isGenderRisk": 1,
  "isPriorityInteraction": 0,
  "pharmacogenomics": [
    {
      "action": "Informative PGx",
      "drug": 3220,
      "gene": "SLCO1B1",
      "guideline": "https://cpicpgx.org/guidelines/cpic-guideline-for-statins/"
    },
    {
      "action": "Informative PGx",
      "drug": 3220,
      "gene": "LDLR",
      "guideline": None
    }
  ]
}
````

fields | type   | description
------ |--------| -----------
"contraindications" | object | Corresponds to user's condition field
"interactionAde" | object | Some possible side effects from interactions
"isGenderRisk" | int    | Is risk gender stratisfied
"isPriorityInteraction" | int    | If it's priority it mustn't be prescribed
"pharmacogenomics" | object | Pharmacogenomics of the drugs
"interactionCount" | int    | How many interactions are in th etherapy
"interactions" | object | The interactions


### contraindications object
fields | type   | description
------ |--------| -----------
"condition" | string | Corresponds to user's condition field
"drug" | int    | Ingredient ID

### interactionAde object
fields | type   | description
------ |--------| -----------
"condition_concept_name" | string | Condition
"drug_1_id" | int    | Ingredient ID
"drug_2_id" | int    | Ingredient ID

### pharmacogenomics object
fields | type   | description
------ |--------| -----------
"action" | string | Importance of the gene drug interaction
"drug" | int    | Ingredient ID
"gene" | string | Gene name
"guideline" | string | Url for action to be taken


### interactions object
fields | type   | description
------ |--------| -----------
"description" | string | Condition
"drug_1_id" | int    | Ingredient ID
"drug_2_id" | int    | Ingredient ID
"id" | int    | Interaction id
"source" | string | source database

### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- PolypharmData API error
403| Error -- Invalid access token

## Scan drug
Evaluates how an addition of a new drug would influence patient's current regimen. It is different from analyze 
is that it returns only the interactions which are between the new drug and the rest of the regimen. It is complementary
to analyze regimen.
<aside class="notice">
Requires an authorization header.
</aside>

### HTTP Request

>Example code

```python
response = requests.get('https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/scan_drug?drug_id=1623', headers=headers)
```

`GET https://polypharm-mobile-api.v9dikv5unmbh4.eu-central-1.cs.amazonlightsail.com/polypharm/scan_drug?drug_id=<param>`

### Query parameters

parameter | type | description        
------ |------| -------------------|
drug_id | int  | Ingredient ID of a scanned drug


### Returns

> GET returns response body

````json
{
  "contraindications": 
    [
      {"condition": "Drug Hypersensitivity", "drug": 1623},
      {"condition": "Hepatic Insufficiency", "drug": 1623}
    ],
  "id": 1623,
  "interactionAde": 
    [
      {
        "condition_concept_name": "Rash maculo-papular",
        "drug_1_id": 1623,
        "drug_2_id": 3220,
        "id": 1567391,
        "significance": 1.993282941489413},
      {
        "condition_concept_name": "Toxic epidermal necrolysis",
        "drug_1_id": 1623,
        "drug_2_id": 3220,
        "id": 1567385,
        "significance": 1.9483149092103744},
      {
        "condition_concept_name": "Pulmonary embolism",
        "drug_1_id": 1623,
        "drug_2_id": 363,
        "id": 601378,
        "significance": 1.8017106054281464},
      {
        "condition_concept_name": "Pyrexia",
        "drug_1_id": 1623,
        "drug_2_id": 1691,
        "id": 2201497,
        "significance": 1.691559012994046
      },
      {
        "condition_concept_name": "Drug interaction",
        "drug_1_id": 1623,
        "drug_2_id": 3220,
        "id": 1567380,
        "significance": 1.6473726786064953
      }
    ],
  "interactionCount": 1,
  "interactions": 
    [
      {
        "description": "Ibuprofen may decrease the excretion rate of Abacavir which could result in a higher serum level.",
        "drug_1_id": 1623,
        "drug_2_id": 1691,
        "id": 1256519,
        "source": "Drugbank"
      }
    ],
  "isGenderRisk": 1,
  "isPriorityInteraction": 0,
  "name": "abacavir",
  "pharmacogenomics": 
    [
      {
        "action": "Testing required",
        "drug": 1623,
        "gene": "HLA-B",
        "guideline": "https://cpicpgx.org/guidelines/guideline-for-abacavir-and-hla-b/"
      }
    ]
}
````

fields | type   | description
------ |--------| -----------
"id" | int    | Ingredient ID
"contraindications" | object | Corresponds to user's condition field
"interactionAde" | object | Some possible side effects from interactions
"isGenderRisk" | int    | Is risk gender stratisfied
"isPriorityInteraction" | int    | If it's priority it mustn't be prescribed
"pharmacogenomics" | object | Pharmacogenomics of the drugs
"interactionCount" | int    | How many interactions are in th etherapy
"interactions" | object | The interactions


### contraindications object
fields | type   | description
------ |--------| -----------
"condition" | string | Corresponds to user's condition field
"drug" | int    | Ingredient ID

### interactionAde object
fields | type   | description
------ |--------| -----------
"condition_concept_name" | string | Condition
"drug_1_id" | int    | Ingredient ID
"drug_2_id" | int    | Ingredient ID

### pharmacogenomics object
fields | type   | description
------ |--------| -----------
"action" | string | Importance of the gene drug interaction
"drug" | int    | Ingredient ID
"gene" | string | Gene name
"guideline" | string | Url for action to be taken


### interactions object
fields | type   | description
------ |--------| -----------
"description" | string | Condition
"drug_1_id" | int    | Ingredient ID
"drug_2_id" | int    | Ingredient ID
"id" | int    | Interaction id
"source" | string | source database

### Response
Code | Meaning
---------- | -------
200| Success
400| Error -- PolypharmData API error
403| Error -- Invalid access token
