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
 - 1st step: 5 min load with 833 Users ![Apache-JMeter-Dashboard-06-02-2025_12_26_PM](https://github.com/user-attachments/assets/56fd7b18-0e3c-44a9-801e-608efc9ea9a1)
 - 2nd step: 10 min load with 1662 Users ![report-05](https://github.com/user-attachments/assets/a6c5a9f0-231d-4a21-8207-b8aaf1dacf8f)
 - 3rd step: 20 min load with 3333 Users ![Screenshot (14)](https://github.com/user-attachments/assets/15837a99-7baf-4bdd-ba2d-2cef5d470f52)

- **Stress Test Statistics from HTML Report**
  Identified the bottleneck throughput by conducting a stress test. ![423141277-38ca8e62-ba85-45e4-ba64-d7046eb72e12](https://github.com/user-attachments/assets/899e3ddd-5fa9-4d27-bda7-f3c32af0eb7a)

  #### Load Test & Stress Test Reports (Excel)
   [Excel Reports](https://docs.google.com/spreadsheets/d/17ooaCxvc1hMH8ib56JXq5pOf8uy16VWmJbgEuoI_OCM/edit?gid=55147309#gid=55147309)
 
![Load-Test-Report-Jmeter-Google-Sheets-06-02-2025_04_00_PM](https://github.com/user-attachments/assets/04bd016e-f0ef-4785-990a-a8e00d9185af)
![Load-Test-Report-Jmeter-Google-Sheets-06-02-2025_04_01_PM](https://github.com/user-attachments/assets/aa5b9cdc-9063-4efd-9e58-3befa8da14a2)



