### 1. System Context Diagram
![PHOTO-2024-12-03-01-39-22](https://github.com/user-attachments/assets/a1fb8c70-9f0d-4f2b-a3b5-936fab38f7a3)
#### Code
```PlantUml
@startuml
!define RECTANGLE class

' External entities
actor "User" as User
actor "Admin" as Admin
actor "Malicious User" as Attacker
entity "Third-Party APIs (Flight, Hotel, Car Rental)" as ExternalServices
entity "Payment Gateway" as PaymentGateway
entity "Cloud Storage" as CloudStorage

' System boundary (Make My Trip Clone)
rectangle "Make My Trip Clone System" {
    usecase "User Registration/Login" as UC1
    usecase "Search & Book Services" as UC2
    usecase "Manage User Profile" as UC3
    usecase "Payments Integration" as UC4
    usecase "Admin Dashboard" as UC5
    usecase "Booking History" as UC6
}

' Relationships
User --> UC1 : "Register/Login"
User --> UC2 : "Search & Book Services"
User --> UC3 : "Update Profile"
User --> UC4 : "Make Payments"
User --> UC6 : "View Booking History"

Admin --> UC5 : "Access Admin Dashboard"
Admin --> UC3 : "Manage User Profiles"

ExternalServices --> UC2 : "Provide Flight, Hotel, and Car Rental Data"
PaymentGateway --> UC4 : "Process Payments"
CloudStorage --> UC6 : "Store Booking Data"

Attacker --> UC1 : "Attempt Brute Force Login"
Attacker --> UC2 : "Submit Fake Bookings"
Attacker --> UC4 : "Attempt Fraudulent Payments"
Attacker --> UC5 : "Unauthorized Admin Access"

@enduml
```
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 2. Container Diagram
![PHOTO-2024-12-03-01-57-05](https://github.com/user-attachments/assets/a52056ec-b1fe-43fb-845c-d229bd011f34)
#### Code
```PlantUml
@startuml
!define RECTANGLE rectangle

title Container Diagram - MakeMyTrip Clone

' Add primary containers
' User section
RECTANGLE "Mobile App" as mobileApp <<Mobile Application>>
RECTANGLE "Web App" as webApp <<Web Application>>
RECTANGLE "User API Gateway" as userGateway <<API Gateway>>

' Backend services
RECTANGLE "Search Service" as searchService <<Microservice>>
RECTANGLE "Booking Service" as bookingService <<Microservice>>
RECTANGLE "Payment Service" as paymentService <<Microservice>>
RECTANGLE "User Service" as userService <<Microservice>>

' Database containers
RECTANGLE "User Database" as userDB <<Database>>
RECTANGLE "Booking Database" as bookingDB <<Database>>
RECTANGLE "Payment Database" as paymentDB <<Database>>

' External systems
RECTANGLE "External Payment Gateway" as paymentGateway <<External System>>
RECTANGLE "Third-Party Travel APIs (Flights, Hotels, Car Rentals)" as travelAPI <<External System>>

' Relationships between containers
mobileApp --> userGateway : "API Calls"
webApp --> userGateway : "API Calls"
userGateway --> searchService : "Search Flights, Hotels, and Car Rentals"
userGateway --> bookingService : "Manage Bookings"
userGateway --> paymentService : "Process Payments"

searchService --> travelAPI : "Fetch Travel Data"
bookingService --> bookingDB : "Read/Write Booking Data"
userService --> userDB : "Read/Write User Data"
paymentService --> paymentDB : "Read/Write Payment Data"

paymentService --> paymentGateway : "Process Payments"
@enduml
```
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 3.1 User component diagram
![PHOTO-2024-12-03-02-02-37](https://github.com/user-attachments/assets/d2e42993-ca4a-47cc-a2b5-072b384e58c8)
#### Code
```PlantUml
@startuml
title Component Diagram - Admin in MakeMyTrip Clone

package "Admin Section" {
    [Admin Dashboard] as adminDashboard
    [Admin API Gateway] as adminGateway

    adminDashboard --> adminGateway : "Admin API Calls"
}

package "Backend Services" {
    [User Management Service] as userManagementService
    [Booking Management Service] as bookingManagementService
    [Report Generation Service] as reportGenerationService
}

package "Databases" {
    [User Database] as userDB
    [Booking Database] as bookingDB
    [Admin Activity Log] as adminActivityLog
}

' Relationships between components
adminGateway --> userManagementService : "Manage User Data"
adminGateway --> bookingManagementService : "Manage Bookings"
adminGateway --> reportGenerationService : "Generate Reports"

userManagementService --> userDB : "Read/Write User Data"
bookingManagementService --> bookingDB : "Read/Write Booking Data"
reportGenerationService --> adminActivityLog : "Log Admin Activities"
@enduml
```
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 3.2 Admin Component Diagram
![c08e4048-1f7b-4dc7-b37c-1a8caa8cac23](https://github.com/user-attachments/assets/980f3710-06e9-4901-9580-af0d558242b0)

#### Code
``` plantuml
@startuml
title Component Diagram - Admin in MakeMyTrip Clone

package "Admin Section" {
    [Admin Dashboard] as adminDashboard
    [Admin API Gateway] as adminGateway

    adminDashboard --> adminGateway : "Admin API Calls"
}

package "Backend Services" {
    [User Management Service] as userManagementService
    [Booking Management Service] as bookingManagementService
    [Report Generation Service] as reportGenerationService
}

package "Databases" {
    [User Database] as userDB
    [Booking Database] as bookingDB
    [Admin Activity Log] as adminActivityLog
}

' Relationships between components
adminGateway --> userManagementService : "Manage User Data"
adminGateway --> bookingManagementService : "Manage Bookings"
adminGateway --> reportGenerationService : "Generate Reports"

userManagementService --> userDB : "Read/Write User Data"
bookingManagementService --> bookingDB : "Read/Write Booking Data"
reportGenerationService --> adminActivityLog : "Log Admin Activities"
@enduml
```
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


### 4. Deployment Diagram
![1c01bd14-4e9b-4a3d-9435-8190db84756f](https://github.com/user-attachments/assets/36f88a86-8c46-4143-8e72-d949b601b0c5)

#### Code
``` plantuml
 @startuml
title Deployment Diagram - MakeMyTrip Clone

node "Web Server" as webServer {
    artifact "Web Application" as webApp
    artifact "User API Gateway" as userAPIGateway
    artifact "Admin API Gateway" as adminAPIGateway
}

node "Mobile Server" as mobileServer {
    artifact "Mobile Application" as mobileApp
    artifact "Mobile API Gateway" as mobileAPIGateway
}

node "Database Server" as dbServer {
    artifact "User Database" as userDB
    artifact "Booking Database" as bookingDB
    artifact "Payment Database" as paymentDB
    artifact "Admin Activity Log" as adminLogDB
}

node "External Services" as externalServices {
    artifact "Third-Party APIs (Flights, Hotels, Rentals)" as externalAPIs
    artifact "Payment Gateway" as paymentGateway
}

' Relationships between nodes and artifacts
webServer --> dbServer : "Request/Store User Data"
webServer --> dbServer : "Request/Store Booking Data"
webServer --> externalServices : "Fetch External Data (Flights, Hotels, Rentals)"
mobileServer --> dbServer : "Request/Store User Data"
mobileServer --> dbServer : "Request/Store Booking Data"
mobileServer --> externalServices : "Fetch External Data (Flights, Hotels, Rentals)"

webServer --> externalServices : "Process Payments"
mobileServer --> externalServices : "Process Payments"

webServer --> dbServer : "Store Admin Activity Logs"
mobileServer --> dbServer : "Store Admin Activity Logs"
@endum
```

