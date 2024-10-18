# Google API Endpoint Documentation
This document provides an overview of the available Google API endpoints, their methods, and the expected responses.

## **Base URL**: `api/auth/v1/google`

## Available endpoints 
- **GET /v1/google**: Kicks off the google auth redirecting you to google page
- **GET /v1/google/callback/failure**: When the google authentication was a failure
- **GET /v1/google/callback/success**: when the google authentication was a success

## **1. Kick off google auth**
### **Endpoint**: `GET /api/v1/google`
### **Description**: Interact with endpoint from a click of a button from client which redirect user to google page for choosing account
### **Response**: There is no response user is being redirected 

## **2. Failure of google auth**
### **Endppoint**: `GET /api/v1/google/failure`
### **Description**: When the auth fails due to some reasons like user rejecting request of permissions or internal server errors

### **Response**:
- **(401 - Unauthorized)**
```json
{
  "status": "Unauthorized",
  "message": "Login Failed",
  "statuscode": 401
}
```
- **(500 - Server Error)**
```json
{
  "status": "Server Error",
  "message": "Error from the server",
  "statuscode": 500
}
```

## **3. Success of google auth**
### **Endppoint**: `GET /api/v1/google/success`
### **Description**: The auth is successful and user logs in

### **Response** (200 - Success):
```json
{
  "status": "Success",
  "message": "Login Successful",
  "user": {
    "firstname": "user firstname",
    "lastname": "user lastname",
    "profilePicture" : "user avatar",
    "email": "user email",
    "phone number": "user phone number",    
  },
    "statuscode": 200,
}
```





