# Performance-Test-Project-Jmeter
## Overview
This repository contains JMeter test plans & reports for performance testing of the **Restful Booker API**
## Pre-requisites
- **Apache JMeter** installed (Latest Version Recommended)
- **Java 8 or later** installed
- **GitHub** installed
- **Internet Connection** (for running API requests)

## Folder Structure
```
.
├── booking.jmx                  # JMeter test plan for Restful Booker API
├── booking-api-test-report.xlsx  # Load & stress test reports in Excel format
├── README.md                     # This file
```

## Instructions to Run Tests
### Task 01: Restful Booker API Performance Testing
1. Open **JMeter**.
2. Load the **bookingApi_test.jmx** file.
3. Configure test execution:
   - Set thread count based on your desired user load.
   - Ensure **Gaussian Random Timer** (Deviation: 2000ms, Constant Delay: 500ms) is used.

4. Run the test and observe the results.

5. Generate reports:
   - Load Test (5min, 10min, 20min load steps)
   - Stress Test (gradually increasing load to find bottleneck)
   - Generate an **HTML Report** and save it.
   - Run the following command in your terminal to execute the JMeter test in **non-GUI mode**: ``` jmeter -n -t .\bookingApi_test.jmx -l .\bookingApi_test.jtl -e -o Reports ```

#### 📌 Command Breakdown:
- `-n` → Non-GUI mode (for faster execution)  
- `-t .\bookingApi_testing.jmx` → Load the test script (`bookingApi_testing.jmx`)  
- `-l .\bookingApi_testing` → Store results in `bookingApi_testing`  
- `-e` → Enable HTML report generation  
- `-o Reports` → Save reports to the `Reports` folder  


## Reports & Screenshots
**Scenario:**
120,000 users over a 12-hour period log in, create a booking, and search for the
booking.

#### Task Overview: 
This test plan (`bookingApi_testing.jmx`) automates API testing for the **RESTful Booker API**, covering:  
✔ Authentication  
✔ Booking creation with **randomized data**  
✔ Booking search and validation  


#### Test Steps & Configuration: 
1️⃣ **Set Headers** (Using HTTP Header Manager)  
   - `Accept: */*`  
2️⃣ **Login & Authentication**  
   - **Endpoint:** `https://restful-booker.herokuapp.com/auth`  
   - **Method:** `POST`  
   - **Request Body:**  
     ``` json:
         {
            "username": "admin",
            "password": "password123"
      
         }
3️⃣ **Create Booking**

   - **Endpoint:**  
   `https://restful-booker.herokuapp.com/booking`
   
   - **Method:**  
   `POST`
   
   **Request Body (Dynamic Data):**  
   ```json
{
   "firstname": "Generate Random FirstName",
   "lastname": "Generate Random LastName",
   "totalprice": "Generate random amount",
   "depositpaid": true,
   "bookingdates": {
      "checkin": "2024-01-01",
      "checkout": "2024-01-02"
   }
}
```
**Extract Booking ID:**  
Use JSON Extractor to capture `bookingid` for validation.

4️⃣ Search Booking

    - **Endpoint:**  
    `https://restful-booker.herokuapp.com/booking/<booking_id>`

    - **Method:**  
    `GET`

**Validation:**  
Ensure the response contains the correct booking details.

#### Load Test & Stress Test Results
- **Request Summary**
 - 1st step: 5 min load with 831 Users ![jmeter 1-1](https://tinyurl.com/2clgvmw9)

