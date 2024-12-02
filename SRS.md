Specification (SRS) for "Make My Trip" Clone

## 1. Introduction

### 1.1 Purpose
This Software Requirements Specification (SRS) document outlines the requirements for the development of a web and mobile application clone of "Make My Trip". The system will enable users to search, book, and manage travel services such as flights, hotels, and car rentals efficiently. The document serves as a comprehensive guide for developers, designers, and stakeholders to ensure clarity of expectations.

### 1.2 Scope
The application will provide the following features:
- User registration and authentication (including social login options).
- Comprehensive search and booking capabilities for flights, hotels, and car rentals.
- Payment processing integration with major payment gateways.
- Profile management for users to track bookings and update details.
- Administrative dashboard for managing users, content, and transactions.
- Compliance with GDPR and other security standards to ensure data protection.

### 1.3 Definitions, Acronyms, and Abbreviations
- **MMT**: Make My Trip  
- **UI**: User Interface  
- **API**: Application Programming Interface  
- **GDPR**: General Data Protection Regulation  
- **2FA**: Two-Factor Authentication  
- **OAuth2**: Open Authorization Protocol  

### 1.4 References
- **SWEBOK**: Software Engineering Body of Knowledge  
- **IEEE 830**: IEEE Recommended Practice for Software Requirements Specifications  
- **WCAG 2.1**: Web Content Accessibility Guidelines  

### 1.5 Overview
This document outlines both functional and non-functional requirements. Functional requirements specify the system's operations and features, while non-functional requirements focus on performance, usability, and compliance.

---

## 2. Overall Description

### 2.1 Product Perspective
The system will be a full-stack solution combining a web-based interface and mobile application. It will integrate with third-party APIs for accessing real-time data on flights, hotels, and car rentals. The platform will emphasize ease of use, security, and scalability to handle high traffic and large datasets.

### 2.2 Product Functions
#### Key Features:
- **Registration/Login**: Secure user account management with social login options.
- **Search**: Intuitive search filters for travel services (flights, hotels, car rentals).
- **Booking**: Secure booking with confirmation emails and in-app notifications.
- **Payments**: Integration with payment gateways for secure and varied payment options.
- **Profile Management**: Enable users to update personal information and view booking history.
- **Admin Tools**: Comprehensive dashboard for managing user data, bookings, and system content.

### 2.3 User Classes and Characteristics
1. **End Users**: General customers who search, book, and manage travel plans.
   - Characteristics: Non-technical, diverse preferences, need user-friendly interfaces.
2. **Admins**: Platform managers who handle backend processes.
   - Characteristics: Technical background, access to secure admin tools.

### 2.4 Operating Environment
- **Frontend**: Web browsers (Chrome, Firefox, Safari) and mobile platforms (iOS, Android).  
- **Backend**: Cloud-hosted web servers with database management systems.  
- **APIs**: Integration with third-party services (e.g., flight/hotel databases).  

### 2.5 Design and Implementation Constraints
- **Third-Party Dependencies**: Reliance on APIs for travel data.  
- **Security Regulations**: Must comply with GDPR and local data protection laws.  
- **Performance Goals**: The system must scale for up to 10,000 concurrent users.  

### 2.6 Assumptions and Dependencies
- Reliable internet connectivity for seamless user experiences.  
- Third-party API availability and reliability.  
- Adherence to evolving legal and regulatory frameworks.  

---

## 3. Functional Requirements

### Use Cases
#### **Use Case 1: User Registration/Login**
- **Actors**: User  
- **Description**: Allows users to create accounts or log in using email or social accounts.  
- **Precondition**: User provides valid credentials.  
- **Postcondition**: User gains access to the platform.  
- **Flow**:  
  - User enters credentials.  
  - System validates credentials.  
  - User is redirected to the dashboard.  
- **Alternative Flow**:  
  - Invalid credentials trigger an error message.  
  - Account lock after five failed attempts.  

#### **Use Case 2: Search for Travel Services**
- **Actors**: User  
- **Description**: Enables users to search for flights, hotels, or car rentals.  
- **Precondition**: Search criteria entered.  
- **Postcondition**: List of options displayed.  
- **Flow**:  
  - User selects filters (dates, locations, price).  
  - System queries external APIs.  
  - Results are displayed with sorting options.  

#### **Use Case 3: Admin Management**
- **Actors**: Admin  
- **Description**: Admins manage users, bookings, and content.  
- **Precondition**: Valid admin login.  
- **Postcondition**: Successful execution of tasks.  
- **Flow**:  
  - Admin selects action (view reports, manage users).  
  - System executes commands and displays results.  

---
### USECASE DIAGRAM
![PHOTO-2024-12-02-22-55-00](https://github.com/user-attachments/assets/69774f79-7da2-43b4-97d7-e6bd70edaa19)

```PlantUml
@startuml
actor "Customer" as Customer
actor "Travel Agent" as Agent
actor "Payment Gateway" as PG
actor "Admin" as Admin

rectangle "MakeMyTrip System" as MakeMyTrip {
  usecase "Search Flights/Hotels" as Search
  usecase "Book Flights/Hotels" as Book
  usecase "Cancel Booking" as Cancel
  usecase "View Booking History" as History
  usecase "Manage Account" as Manage
  usecase "Apply Promo Code" as Promo
  usecase "Generate Reports" as Reports
  usecase "Assist Customer" as Assist
  usecase "Handle Refunds" as Refund
}

Customer --> Search : "Initiate Search"
Customer --> Book : "Proceed to Book"
Customer --> Cancel : "Request Cancellation"
Customer --> History : "Access Booking History"
Customer --> Manage : "Update Profile"
Customer --> Promo : "Apply Discounts"

Agent --> Search : "Perform Search"
Agent --> Book : "Assist Booking"
Agent --> Assist : "Provide Support"

Book --> PG : "Process Payment"
Book --> Promo : "Validate Promo Code"
Cancel --> Refund : "Initiate Refund"

Admin --> Reports : "Analyze Data"
Admin --> Assist : "Resolve Issues"
Admin --> Refund : "Approve Refunds"
@enduml
```
## 4. Error Cases

### Use Cases for Error Scenarios
#### **Authentication Errors**
- **Invalid Credentials**: User enters invalid login credentials.
- **Account Locked After Repeated Failures**: User is locked out after multiple incorrect login attempts.
- **Session Timeout**: User session expires due to inactivity.
- **2FA Code Expired**: Two-Factor Authentication code has expired.

#### **Booking Errors**
- **Invalid Search Criteria**: Invalid search filters or criteria entered by the user.
- **Overbooking**: The booking fails due to no available capacity for the selected service.
- **API Failure for External Services**: The system fails to retrieve data from external services (e.g., flight, hotel).
- **Incomplete Booking Details**: Missing or incomplete information required for booking.

#### **Payment Errors**
- **Card Declined**: Payment is declined by the user's bank or card issuer.
- **Insufficient Funds**: The user does not have enough funds for the transaction.
- **Payment Gateway Timeout**: The payment gateway times out while processing the transaction.
- **Duplicate Transaction**: A duplicate payment is detected.

#### **Admin Errors**
- **Unauthorized Admin Access Attempt**: A malicious user attempts to gain unauthorized admin access.
- **Failure to Load Reports**: Admin is unable to load reports due to system errors or maintenance.
- **Error in User Management Actions**: An admin encounters issues while managing users.
- **Data Sync Issues with Backup Server**: The system encounters problems syncing data with the backup server.

---
 ![image](https://github.com/user-attachments/assets/34639c59-a5e5-4a95-835a-e09467ac5131)
```PlantUml
@startuml
left to right direction

actor "Legitimate User" as User
actor "Malicious User" as Attacker
actor "Administrator" as Admin

rectangle "Make My Trip Clone  " {
    rectangle "Core Functionalities" as CF {
        usecase "Register/Login" as UC1
        usecase "Search & Book Services" as UC2
        usecase "Make Secure Payments" as UC3
        usecase "Access Admin Dashboard" as UC4
        usecase "Cancel or Modify Booking" as UC5
        usecase "View Booking History" as UC6
        usecase "Manage User Profile" as UC7
    }

    rectangle "Abuse Prevention System" as APS {
        usecase "Prevent Brute Force Attacks" as APS1
        usecase "Validate Booking Details" as APS2
        usecase "Detect Fraudulent Payment Patterns" as APS3
        usecase "Monitor Admin Login Attempts" as APS4
        usecase "Blacklist Suspicious IPs" as APS5
        usecase "Enable Two-Factor Authentication (2FA)" as APS6
        usecase "Implement Data Input Sanitization" as APS7
    }
}

User --> UC1 : "Log In"
User --> UC2 : "Search and Book Services"
User --> UC3 : "Make Payments"
User --> UC5 : "Cancel or Reschedule Booking"
User --> UC6 : "View Booking History"
User --> UC7 : "Update Profile"

Attacker --> UC1 : "Brute Force Login"
Attacker --> UC2 : "Submit Fake Bookings"
Attacker --> UC3 : "Fraudulent Payment Attempts"
Attacker --> UC4 : "Unauthorized Admin Access"
Attacker --> UC5 : "Exploit Cancellation Policies"
Attacker --> UC7 : "Inject Malicious Data"

APS1 --> UC1 : "Block Repeated Failed Logins"
APS2 --> UC2 : "Verify Booking Parameters"
APS3 --> UC3 : "Analyze Payment Patterns"
APS4 --> UC4 : "Restrict Admin Access by Role/IP"
APS5 --> UC1 : "Blacklist Malicious IPs"
APS6 --> UC1 : "Secure Login with 2FA"
APS7 --> UC7 : "Sanitize Inputs to Prevent Injection"

Admin --> UC4 : "Access Admin Panel"
Admin --> UC5 : "Oversee Cancellations"
Admin --> UC7 : "Monitor Suspicious Activities"
@enduml
```
## 5. Abuse Prevention System

### Use Cases for Abuse Prevention
#### **Brute Force Attack Prevention**
- **Prevent Brute Force Attacks**: The system blocks repeated login attempts after a specified number of failed attempts.
  
#### **Booking and Payment Fraud Prevention**
- **Validate Booking Details**: Ensure the booking details provided by the user are correct and valid.
- **Detect Fraudulent Payment Patterns**: Monitor payment transactions for unusual or fraudulent activities.

#### **Admin Security and Monitoring**
- **Monitor Admin Login Attempts**: The system tracks and monitors suspicious admin login attempts.
- **Blacklist Suspicious IPs**: Malicious IP addresses are blocked from accessing the system.

#### **General Security Measures**
- **Enable Two-Factor Authentication (2FA)**: Additional security layer for user login via 2FA.
- **Implement Data Input Sanitization**: Prevent malicious code injection and ensure data integrity by sanitizing inputs.

### Use Cases for Abuse by Malicious Users
- **Brute Force Login**: A malicious user attempts to gain access through repeated login attempts.
- **Submit Fake Bookings**: Malicious users try to exploit booking functionality by submitting fake or incorrect booking details.
- **Fraudulent Payment Attempts**: Users attempt to make payments using stolen or invalid payment information.
- **Unauthorized Admin Access**: Malicious users attempt to bypass admin login or perform unauthorized actions.
- **Exploit Cancellation Policies**: Malicious users take advantage of cancellation policies for fraudulent refunds or bookings.
- **Inject Malicious Data**: Users attempt to inject harmful code into the system to exploit security vulnerabilities.

--- 
![image](https://github.com/user-attachments/assets/578a8e2c-b652-4c21-9599-704ef7ba1ac8)

```plantuml
@startuml
left to right direction

actor "Legitimate User" as User
actor "Malicious User" as Attacker
actor "Administrator" as Admin

rectangle "Make My Trip Clone" {
    rectangle "Core Functionalities" as CF {
        usecase "Register/Login" as UC1
        usecase "Search & Book Services" as UC2
        usecase "Make Secure Payments" as UC3
        usecase "Access Admin Dashboard" as UC4
        usecase "Cancel or Modify Booking" as UC5
        usecase "View Booking History" as UC6
        usecase "Manage User Profile" as UC7
    }

    rectangle "Abuse Prevention System" as APS {
        usecase "Prevent Brute Force Attacks" as APS1
        usecase "Validate Booking Details" as APS2
        usecase "Detect Fraudulent Payment Patterns" as APS3
        usecase "Monitor Admin Login Attempts" as APS4
        usecase "Blacklist Suspicious IPs" as APS5
        usecase "Enable Two-Factor Authentication (2FA)" as APS6
        usecase "Implement Data Input Sanitization" as APS7
    }
}

User --> UC1 : "Log In"
User --> UC2 : "Search and Book Services"
User --> UC3 : "Make Payments"
User --> UC5 : "Cancel or Reschedule Booking"
User --> UC6 : "View Booking History"
User --> UC7 : "Update Profile"

Attacker --> UC1 : "Brute Force Login"
Attacker --> UC2 : "Submit Fake Bookings"
Attacker --> UC3 : "Fraudulent Payment Attempts"
Attacker --> UC4 : "Unauthorized Admin Access"
Attacker --> UC5 : "Exploit Cancellation Policies"
Attacker --> UC7 : "Inject Malicious Data"

APS1 --> UC1 : "Block Repeated Failed Logins"
APS2 --> UC2 : "Verify Booking Parameters"
APS3 --> UC3 : "Analyze Payment Patterns"
APS4 --> UC4 : "Restrict Admin Access by Role/IP"
APS5 --> UC1 : "Blacklist Malicious IPs"
APS6 --> UC1 : "Secure Login with 2FA"
APS7 --> UC7 : "Sanitize Inputs to Prevent Injection"

Admin --> UC4 : "Access Admin Panel"
Admin --> UC5 : "Oversee Cancellations"
Admin --> UC7 : "Monitor Suspicious Activities"

@enduml
```
## 6. Non-Functional Requirements

### Performance
- **Response Time**: The system processes user actions within 2 seconds.  
- **Scalability**: Can handle up to 10,000 concurrent users.  

### Security
- **Authentication**: OAuth2 and 2FA implementation.  
- **Encryption**: Secure all sensitive data.  
- **Authorization**: Role-based access control.  

### Usability
- **Intuitive UI**: Easy-to-navigate interface for diverse user groups.  
- **Accessibility**: WCAG 2.1 compliance for users with disabilities.  

### Reliability
- **Uptime**: 99.9% availability.  
- **Data Backup**: Regular data backups to prevent loss.  

### Compliance
- **GDPR Compliance**: Adhere to global and local data protection regulations.  

---

## 7. Other Requirements

### 7.1 Data Requirements
- **Schema**: Efficient data storage for user profiles, transactions, and history.  
- **Backup**: Automated hourly backups.  

### 7.2 Interface Requirements
- **APIs**: Seamless integration with external travel and payment services.  
- **Admin Panel**: Secure access for platform management.  

### 7.3 Environmental Requirements
- **Cloud Hosting**: Deploy on scalable, secure cloud services.  
- **Mobile Optimization**: Fully functional on both iOS and Android platforms.  

---

