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
   - Run the following command in your terminal to execute the JMeter test in **non-GUI mode**: ``` jmeter -n -t .\booking.jmx -l .\booking.jtl -e -o Reports ```

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
