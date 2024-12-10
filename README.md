# **Rest Booking API Testing with Postman and Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

## What is API And API Testing ?

**API(Application Programming Interface)**: A bridge that allows different software systems to communicate and exchange data.

**API Testing**: Checking if an API works correctly, returns expected results, and handles errors and security properly.

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- https://github.com(Wait)
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation(How to Run Project)**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/Mahmuduls1995/API-Testing-of-Rest-BookingAPI-With-Postman-Newman.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**

1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing Process**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
var firstName = pm.variables.replaceIn("{{$randomFirstName}}");
console.log(firstName);
pm.environment.set("firstname", firstName);

var lastName=pm.variables.replaceIn("{{$randomLastName}}");
console.log(lastName);
pm.environment.set("lastname",lastName);


var totalPrice=pm.variables.replaceIn("{{$randomInt}}")
console.log(totalPrice)
pm.environment.set("totalprice",totalPrice);

var depositPaid=pm.variables.replaceIn("{{$randomBoolean}}");
console.log(depositPaid)
pm.environment.set("depositpaid",depositPaid);

const moment = require('moment')
const today = moment();
var checkin=today.add(2,'d').add(1,'M').format("YYYY-MM-DD")
pm.environment.set('checkin',checkin)

var checkOut=today.subtract(2, 'months').subtract(5, 'd').format("yyyy-MM-DD")
pm.environment.set('checkout',checkOut)

var additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")
pm.environment.set("additionalNeeds", additionalNeeds)
```
  **Request Body:** 
 ```console 
{
    "firstname": "{{firstname}}",
    "lastname": "{{lastname}}",
    "totalprice": {{totalprice}},
    "depositpaid": {{depositpaid}},
    "bookingdates": {
               "checkin": "{{checkin}}",
                "checkout": "{{checkout}}"
    },
     "additionalneeds" : "{{additionalNeeds}}"
}
```
  **Response Body:**
 ```console 
{
    "bookingid": 954,
    "booking": {
        "firstname": "Murray",
        "lastname": "Goodwin",
        "totalprice": 685,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2025-01-12",
            "checkout": "2024-11-07"
        },
        "additionalneeds": "bus"
    }
}
```
## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Murray",
    "lastname": "Goodwin",
    "totalprice": 685,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-01-12",
        "checkout": "2024-11-07"
    },
    "additionalneeds": "bus"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "06eb798bf6f2caa"
}
```
## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
    var update_firstName = pm.variables.replaceIn("{{$randomFirstName}}");
pm.environment.set("update_firstname", update_firstName);

var update_lastName=pm.variables.replaceIn("{{$randomLastName}}");
pm.environment.set("update_lastname",update_lastName);


var update_totalPrice=pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("update_totalprice",update_totalPrice);

var update_depositPaid=pm.variables.replaceIn("{{$randomBoolean}}");
pm.environment.set("update_depositpaid",update_depositPaid);

const moment = require('moment')
const today = moment();

var update_checkIn=today.add(4,'d').format("YYYY-MM-DD")
pm.environment.set('update_checkin',update_checkIn)

    
var update_checkOut=today.format("YYYY-MM-DD")
pm.environment.set('update_checkout',update_checkOut)

var update_additionalneeds=pm.variables.replaceIn("{{$randomNoun}}");
pm.environment.set("update_additionalNeeds",update_additionalneeds);

```
  **Request Body:** 
 ```console 
  {
    "firstname": "{{update_firstname}}",
    "lastname": "{{update_lastname}}",
    "totalprice": {{update_totalprice}},
    "depositpaid": {{update_depositpaid}},
    "bookingdates": {
        "checkin": "{{update_checkin}}",
        "checkout": "{{update_checkout}}"
    },
     "additionalneeds" : "{{update_additionalNeeds}}"
} 
```
  **Response Body:**
 ```console 
  {
    "firstname": "Dulce",
    "lastname": "Cruickshank",
    "totalprice": 487,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-12-14",
        "checkout": "2024-12-14"
    },
    "additionalneeds": "microchip"
}
```
## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run API_Project_1st.postman_collection.json -e API_Project_1st_Env.postman_environment.json 
```
![console-result](https://github.com/user-attachments/assets/2f41c211-be82-4ce6-9e84-889a9949c8a7)
 | 
![image](https://github.com/user-attachments/assets/21d00ae1-1b55-402e-b2c7-6ed544f69b04)

- Run Command for Report html:
```console 
newman run API_Project_1st.postman_collection.json -e API_Project_1st_Env.postman_environment.json -r html
```
### Newman HTML Report

![newman-html-report](https://github.com/user-attachments/assets/d8bc8e0d-0420-4b4a-9892-b74c5d4c943c)

- Run Command for Report htmlextra
```console 
newman run API_Project_1st.postman_collection.json -e API_Project_1st_Env.postman_environment.json -r htmlextra
```
