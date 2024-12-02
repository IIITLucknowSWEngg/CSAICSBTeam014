# Software Requirements Specification (SRS) for "Make My Trip" Clone

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


