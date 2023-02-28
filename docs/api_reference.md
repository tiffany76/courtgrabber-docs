## Overview of the Courtgrabber REST API

The following documentation explains the Courtgrabber REST API. If you would like to use the Courtgrabber CLI, please refer to the [user guide](./user_guide.md). 

The Courtgrabber API is an HTTP-based, RESTful service that interfaces with tennis club reservation software to make court reservations on behalf of club members. Most club software sets a reservation window. With Courtgrabber, users can submit a request outside that window, automating the reservation process.

Courtgrabber's base URL is [https://courtgrabber.herokuapp.com/api/](https://courtgrabber.herokuapp.com/api/). The API has five endpoints, and it accepts JSON in request bodies and returns JSON in response bodies. 

### Workflow 

A user's typical workflow might look like this: login to Courtgrabber, add a new reservation request, verify that the request was successful, and then logout. Here are the corresponding API calls for these tasks:

- [`POST /login`](#logging-into-courtgrabber)
- [`POST /reservation-requests`](#requesting-a-tennis-court-reservation)
- [`GET /reservation-requests`](#retrieving-a-list-of-reservation-requests)
- [`POST /logout`](#logging-out-of-courtgrabber)

Users can also cancel pending requests. That API call is [`DELETE /api/reservation-requests/{id}`](#canceling-a-reservation-request).

### Authentication

The first call to `/login` specifies the member's club email address and password as a JSON object in the body. A response of `200 OK` includes a bearer token with a validity of 30 minutes. All other endpoints, including `/logout`, take the bearer token in the header (`Authorization: Bearer {token}`). Each use of the token, except with `/logout`, extends the token's validity for another 30 minutes.

## Courtgrabber API reference documentation

This section explains Courtgrabber's resources, endpoints, and status codes.

  * [Resources](#resources)
  * [Logging into Courtgrabber](#logging-into-courtgrabber)
  * [Requesting a tennis court reservation](#requesting-a-tennis-court-reservation)
  * [Retrieving a list of reservation requests](#retrieving-a-list-of-reservation-requests)
  * [Canceling a reservation request](#canceling-a-reservation-request)
  * [Logging out of Courtgrabber](#logging-out-of-courtgrabber)
  * [Status codes and error messages](#status-codes-and-error-messages)

### Resources

The Courtgrabber API has three resources:

- `/api/login`
- `/api/logout`
- `/api/reservation-requests`

#### `/api/login`
Use the Login API call to grant a club member access to Courtgrabber.

#### `/api/logout`
Use the Logout API call to terminate the current Courtgrabber session.

#### `/api/reservation-requests`
Reservation Requests is the core Courtgrabber resource. Use API calls against it to create new requests, view existing requests, or cancel requests. 

### Logging into Courtgrabber
Authenticates a user and grants them access for a Courtgrabber session.

#### URL
```
POST {base_url}/api/login
```

#### Request Body

| **Field**      |   **Description**                        | **Type**  | **Required**   |
| ---------------| ---------------------------------------- | --------- | -------------- |
| username       | User's tennis club account email address | string    | Required       |
| password       | User's tennis club account email password| string    | Required       |

#### Sample Request
```
POST {base_url}/api/login
```
```json
{
    "username": "member@tennisclub.com",
    "password": "***************"    
}
```

#### Response Body

| **Field**            |   **Description**                                      | **Type**  | 
| -------------------- | ------------------------------------------------------ | --------- | 
| bearer_token         | Authorizes access to authenticated user for 30 minutes | string    | 

#### Sample Response
```
200 OK
```
```json
{
    "bearer_token": "Y0jzJLkuhPudMf9J"
}
```

### Requesting a tennis court reservation
Initiates a reservation request to the tennis club's software.

#### URL
```
POST {base_url}/api/reservation-requests
```

#### Headers

| **Header Name**                    |   **Description**                                    | **Required** | **Values**      |
| ---------------------------------- | ---------------------------------------------------- | ------------ | --------------- |
| [Authorization](#authentication)   | Credentials to authenticate user with server         | Required     | Bearer: {token} |

#### Request Body

| **Field**  |   **Description**                             | **Type**         | **Required**  | **Notes**          |
| ---------- | --------------------------------------------- | ---------------- | ------------- | -----------------  |
| date       | Date to reserve tennis court                  | string           | Required      | Format: YYYY-MM-DD |
| start_times | Time to reserve tennis court, in order of preference | array of strings | Required | Format: HHMM in 24H time |
| duration   | Length of time to reserve tennis court        | string           | Required      | Values: 30m, 60m, 90m |
| courts     | Tennis court number to reserve, in order of preference | array of numbers | Required | 
| ball_machine | Reserve ball machine along with court       | Boolean          | Required      |
| players    | Club members who will play, with host listed first | array of strings | Required | Values: members linked to login account |

#### Sample Request
```
POST {base_url}/api/reservation-requests
Authorization: Bearer: {token}
```
```json
{
    "date": "2022-12-09",
    "start_times": [
        "1000",
        "1030"
    ],
    "duration": "90m",
    "courts": [
        1,
        2
    ],
    "ball_machine": false,
    "players": [
        "Alice Jones",
        "Bob Jones"
    ]
}
```

#### Response Body

| **Field**     |   **Description**                           | **Type**  | **Notes**                      |
| ------------- | ------------------------------------------- | --------- | ------------------------------ |
| id            | Unique identifier for a reservation request | string    |
| date          | Date to reserve tennis court                | string    | Format: YYYY-MM-DD             |
| start_times   | Time to reserve tennis court, in order of preference | array of strings | Format: HHMM in 24H time |
| duration      | Length of time to reserve tennis court      | string    | Values: 30m, 60m, 90m          |
| courts        | Tennis court number to reserve, in order of preference | array of numbers |  
| ball_machine  | Reserve ball machine along with court       | Boolean   | 
| players       | Club members who will play, with host listed first | array of strings | Values: members linked to login account |

#### Sample Response
```
200 OK
```
```json
{
    "id": "e68bfb6d-a1f0-4e8a-b82f-4acbbcc3397b",
    "date": "2022-12-09",
    "start_times": [
        "1000",
        "1030"
    ],
    "duration": "90m",
    "courts": [
        1,
        2
    ],
    "ball_machine": false,
    "players": [
        "Alice Jones",
        "Bob Jones"
    ]
}
```

### Retrieving a list of reservation requests
Returns the user's reservation requests.

#### URL
```
GET {base_url}/api/reservation-requests
```

#### Headers

| **Header Name**                    |   **Description**                                    | **Required** | **Values**      |
| ---------------------------------- | ---------------------------------------------------- | ------------ | --------------- |
| [Authorization](#authentication)   | Credentials to authenticate user with server         | Required     | Bearer: {token} |

#### Sample Request
```
GET {base_url}/api/reservation-requests 
Authorization: Bearer: {token}
```

#### Response Body

| **Field**            |   **Description**                                  | **Type**  | **Notes**                 |
| -------------------- | -------------------------------------------------- | --------- | ------------------------- |
| reservation-requests | Data on when, where, and for whom to reserve court | array     |                           |
| id                   | Unique identifier for reservation request          | string    |                           |
| date                 | Date to reserve tennis court                       | string    | Format: YYYY-MM-DD        |
| start_times          | Time to reserve tennis court, in order of preference | array of strings | Format: HHMM in 24H time |
| duration             | Length of time to reserve tennis court             | string    | Values: 30m, 60m, 90m     |
| courts               | Tennis court number to reserve, in order of preference | array of numbers |  
| ball_machine         | Reserve ball machine along with court              | Boolean   | 
| players              | Club members who will play, with host listed first | array of strings | Values: members linked to login account |
| court                | The court number that was successfully reserved    | number    |                           |
| start_time           | The start time that was successfully reserved      | string    | Format: ISO 8601 YYYY-MM-DDThh:mm:ssTZD |

#### Sample Response
```
200 OK
```
```json
{
    "reservation-requests": [
        {
            "id": "e68bfb6d-a1f0-4e8a-b82f-4acbbcc3397b",
            "date": "2022-12-05",
            "start_times": [
                "0700"
            ],
            "duration": "90m",
            "courts": [
                5,
                9
            ],
            "ball_machine": true,
            "players": [
                "Alice Jones",
                "Bob Jones"
            ]
        },
        {
            "id": "7c98610d-2429-4ed8-8cc2-33123e8a6fa9",
            "date": "2022-11-19",
            "start_times": [
                "1300",
                "1330",
                "1400"
            ],
            "duration": "90m",
            "courts": [
                1,
                2,
                3
            ],
            "ball_machine": false,
            "players": [
                "Carrie Jones",
                "Alice Jones"
            ],
            "court": 1,
            "start_time": "2022-11-19T13:00:00-08:00"
        }
    ]
}
```

### Canceling a reservation request
Deletes a pending reservation request. 

> **NOTE**: Requests that secure a court reservation cannot be canceled through Courtgrabber; they must be canceled in the tennis club's software.

#### URL
```
DELETE {base_url}/api/reservation-requests/{id}
```

#### Parameter

| **Parameter**   |   **Description**                           | **Type** | **Required**    |
| --------------- | ------------------------------------------- | -------- | --------------- |
|  id             | Unique identifier for a reservation request | string   | Required        |

#### Headers

| **Header Name**                    |   **Description**                                    | **Required** | **Values**      |
| ---------------------------------- | ---------------------------------------------------- | ------------ | --------------- |
| [Authorization](#authentication)   | Credentials to authenticate user with server         | Required     | Bearer: {token} |

#### Sample Request
```
DELETE {base_url}/api/reservation-requests/e68bfb6d-a1f0-4e8a-b82f-4acbbcc3397b
Authorization: Bearer: {token}
```

#### Response Body

| **Field**            |   **Description**              | **Type**  | **Notes**                                         |
| -------------------- | -------------------------------| --------- | ------------------------------------------------- |
| message              | Status of delete request       | string    | Values: reservation request deleted; delete failed|

#### Sample Response
```
200 OK
```
```json
{
    "message": "reservation request deleted"
}
```

### Logging out of Courtgrabber
Terminates a Courtgrabber session. 

#### URL
```
POST {base_url}/api/logout
```

#### Headers

| **Header Name**                    |   **Description**                                    | **Required** | **Values**      |
| ---------------------------------- | ---------------------------------------------------- | ------------ | --------------- |
| [Authorization](#authentication)   | Credentials to authenticate user with server         | Required     | Bearer: {token} |

#### Sample Request
```
POST {base_url}/api/logout
Authorization: Bearer: {token}
```

#### Sample Response
```
204 No Content
```

### Status codes and error messages
The following table lists the HTTP status codes and their meanings. 

| **Code**             |   **Description**                                                                       | 
| -------------------- | --------------------------------------------------------------------------------------- | 
| 200 OK               | Call was successful: if relevant, response details included in body                     | 
| 204 No Content       | Call was successful: no details provided in response                                    |  
| 400 Bad Request      | Call was unsuccessful: required field(s) omitted                                        |  
| 404 Not Found        | Call was unsuccessful: incorrect endpoint used                                          |  

For unsuccessful calls, the API will return the corresponding HTTP status code with this response body:

```json
{
    "message": "<some error message>"
} 
```
