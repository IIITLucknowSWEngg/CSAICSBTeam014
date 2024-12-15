# MakeMyTrip Competitor Booking System Architecture

## 1. Context Diagram
A context diagram for the MakeMyTrip Competitor Booking System illustrates its interactions with external entities. The main system is the "MakeMyTrip Competitor Booking System," surrounded by entities such as "Customer," "Payment Gateway," "Hotel," and "Inventory System." The arrows represent information flow between the main system and external entities. The diagram provides a high-level view of the system's scope and relationships, facilitating understanding among stakeholders.

![image](https://github.com/user-attachments/assets/0f88feae-c443-4c20-b532-c4613f4f5431)

#### Code
```
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

LAYOUT_TOP_DOWN()
title System Context Diagram - MakeMyTrip Competitor Booking System

Person(customer, "Customer", "Searches, books, and manages travel bookings")
Person(hotelAdmin, "Hotel Admin", "Manages hotel details, room availability, and pricing")

System(competitorBookingSystem, "MakeMyTrip Competitor Booking System", "Online platform for booking hotels, flights, and vacation packages")

System_Ext(paymentGateway, "Payment Gateway", "Processes customer payments securely")
System_Ext(hotel, "Hotel", "Provides accommodations")
System_Ext(inventorySystem, "Inventory System", "Tracks room availability and pricing")
System_Ext(notificationService, "Notification Service", "Sends booking confirmations and alerts")
System_Ext(analytics, "Analytics", "Tracks user behavior and platform performance")
System_Ext(reviewSystem, "Review System", "Manages customer feedback and ratings")
System_Ext(flightService, "Flight Service", "Provides flight details and booking options")

Rel(customer, competitorBookingSystem, "Searches, books, and manages travel bookings", "HTTPS")
Rel(hotelAdmin, competitorBookingSystem, "Manages hotel details and inventory", "HTTPS")
Rel(competitorBookingSystem, paymentGateway, "Processes payments", "API")
Rel(competitorBookingSystem, hotel, "Sends booking details", "API")
Rel(competitorBookingSystem, inventorySystem, "Syncs room availability and pricing", "API")
Rel(competitorBookingSystem, notificationService, "Sends booking confirmations", "SMTP")
Rel(competitorBookingSystem, analytics, "Tracks platform usage", "API")
Rel(competitorBookingSystem, reviewSystem, "Manages customer feedback", "API")
Rel(competitorBookingSystem, flightService, "Handles flight bookings", "API")
@enduml
```
---
## 2. Container Diagram
The container diagram for the MakeMyTrip Competitor Booking System shows the software containers that make up the system. The main containers are the "Web Frontend," "Booking Service," "Payment Service," "Flight Service," and "Database." The "Web Browser" interacts with the "Web Frontend" for user interaction. The "Booking Service" and "Payment Service" handle booking and payment processes. The "Flight Service" handles flight bookings, and the "Database" stores system data. The diagram illustrates the system's software architecture and component relationships.

![image](https://github.com/user-attachments/assets/16bfc3c7-0c57-4698-aa51-1f8b0f66098c)

#### Code
```
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

skinparam {
    RectangleBackgroundColor #C08080
    RectangleBorderColor #A06060
    RectangleFontColor #FFFFFF
    ArrowColor #A06060
    ArrowThickness 2
    ArrowStyle dashed
}

LAYOUT_TOP_DOWN()
title Container Diagram - MakeMyTrip Competitor Booking System

Person(customer, "Customer", "Searches, books, and manages travel bookings")
Person(hotelAdmin, "Hotel Admin", "Manages hotel details, room availability, and pricing")

System_Boundary(competitorBookingSystem, "MakeMyTrip Competitor Booking System") {
    Container(webFrontend, "Web Frontend", "React", "Allows customers to search and book hotels, flights, and packages")
    Container(bookingService, "Booking Service", "Node.js", "Handles hotel and flight booking operations")
    Container(paymentService, "Payment Service", "Java", "Processes payments securely")
    Container(notificationService, "Notification Service", "Python", "Sends booking confirmations and notifications")
    Container(flightService, "Flight Service", "Ruby", "Handles flight bookings and management")
    
    ContainerDb(mainDatabase, "Database", "PostgreSQL", "Stores customer, booking, hotel, and flight data")
}

System_Ext(paymentGateway, "Payment Gateway", "Processes customer payments securely")
System_Ext(hotel, "Hotel", "Provides accommodations")
System_Ext(inventorySystem, "Inventory System", "Tracks room availability and pricing")
System_Ext(flightServiceAPI, "Flight Service API", "Provides flight booking options")

Rel(customer, webFrontend, "Interacts with", "HTTPS")
Rel(hotelAdmin, competitorBookingSystem, "Manages hotel details and inventory", "HTTPS")
Rel(webFrontend, bookingService, "Handles booking requests", "HTTPS")
Rel(webFrontend, paymentService, "Processes payments", "HTTPS")
Rel(bookingService, mainDatabase, "Stores booking data", "JDBC")
Rel(paymentService, paymentGateway, "Processes payments", "API")
Rel(notificationService, mainDatabase, "Fetches booking data", "JDBC")
Rel(notificationService, customer, "Sends notifications", "SMTP")
Rel(bookingService, inventorySystem, "Updates room availability", "API")
Rel(bookingService, flightServiceAPI, "Fetches flight details", "API")
@enduml
```
---
## 3. Component Diagram
i) **User Features**
![image](https://github.com/user-attachments/assets/ce21c849-c286-4b12-a23a-c5f73a067d82)

#### Code
```@startuml
' Component Diagram for User Features of MakeMyTrip Competitor

skinparam componentStyle rectangle

' External User
actor "User" as User

' Components
component "UI Layer" as UI
component "Search & Filter Service" as SFS
component "Booking Service" as BS
component "Payment Gateway" as PG
component "Recommendation Service" as RS
component "Notification Service" as NS
component "Reviews & Ratings Service" as RRS

' Databases
database "Room Listings DB" as RDB
database "Booking DB" as BDB
database "User Reviews DB" as CRDB
database "Flight Listings DB" as FDB

' Relationships
user --> UI : "Interacts"
UI --> SFS : "Searches and filters rooms"
UI --> BS : "Makes bookings"
UI --> PG : "Processes payments"
UI --> RS : "Receives recommendations"
UI --> NS : "Receives notifications"
UI --> RRS : "Leaves reviews"

' Database Connections
SFS --> RDB : "Fetches room details"
SFS --> FDB : "Fetches flight details"
BS --> BDB : "Stores booking details"
PG --> BDB : "Processes payments"
RRS --> CRDB : "Stores reviews and ratings"

@enduml
```
---
ii) **Admin Features**
![image](https://github.com/user-attachments/assets/852f8fce-96db-4963-84fc-e81b09c421a5)
#### Code
```
@startuml
' Component Diagram for Admin Features of MakeMyTrip Competitor

skinparam componentStyle rectangle

' External Actor
actor "Admin" as admin

' Components
component "Admin Dashboard" as AD
component "Room Management Service" as RMS
component "User Management Service" as UMS
component "Booking Management Service" as BMS
component "Analytics Service" as AS
component "Notification Service" as NS

' Databases
database "Room Listings DB" as RDB
database "User DB" as UDB
database "Booking DB" as BDB
database "Flight Listings DB" as FDB

' Relationships
admin --> AD : "Accesses"
AD --> RMS : "Manages room details"
AD --> UMS : "Manages users"
AD --> BMS : "Manages bookings"
AD --> AS : "Views analytics"
AD --> NS : "Sends notifications"

' Database Connections
RMS --> RDB : "Adds/Edits/Deletes room listings"
UMS --> UDB : "Accesses user details"
BMS --> BDB : "Updates booking statuses"
AS --> RDB : "Fetches room data"
AS --> BDB : "Fetches booking data"
AS --> UDB : "Fetches user activity"

@enduml
```
---
## 4. Deployment Diagram

A deployment diagram for the MakeMyTrip Competitor Booking System illustrates the physical architecture of the system, showing how different components are deployed across nodes. The diagram includes key tiers such as the "Client Tier" with web and mobile apps, the "API Tier" with services like API Gateway, Booking Service, and Flight Service, and the "Data Tier" with databases for user, booking, and flight data. Additionally, the diagram includes Non-Functional Requirements (NFRs) like scalability, security, and performance monitoring.

![image](https://github.com/user-attachments/assets/c492ffd8-f485-49f9-95ac-b7954ed4117f)

#### Code
```
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Deployment.puml

LAYOUT_WITH_LEGEND()
title Deployment Diagram - MakeMyTrip Competitor Booking System

Deployment_Node(client, "Client Tier", "User Devices") {
    Deployment_Node(browser, "Web Browser") {
        Container(web, "Web App", "React", "Allows users to search and book hotels, flights, and packages")
    }
    Deployment_Node(mobile, "Mobile Device") {
        Container(app, "Mobile App", "React Native", "Provides hotel search and booking on the go")
    }
}

Deployment_Node(api, "API Tier", "AWS ECS/Kubernetes") {
    Deployment_Node(api_cluster, "API Cluster", "Load Balanced") {
        Container(api_gateway, "API Gateway", "Express.js", "Handles incoming requests and routing")
        Container(booking_service, "Booking Service", "Node.js", "Manages hotel bookings and availability")
        Container(auth_service, "Authentication Service", "OAuth2/OpenID", "Handles user authentication and sessions")
        Container(flight_service, "Flight Service", "Ruby", "Handles flight bookings and management")
    }
    Deployment_Node(notification, "Notification Service") {
        Container(notification_service, "Notification Service", "Python", "Sends booking confirmations and alerts")
    }
}

Deployment_Node(data, "Data Tier", "AWS RDS/DynamoDB") {
    Deployment_Node(databases, "Database Cluster") {
        ContainerDb(user_db, "User Database", "Amazon RDS", "Stores user information")
        ContainerDb(booking_db, "Booking Database", "Amazon RDS", "Stores booking details and hotel availability")
        ContainerDb(flight_db, "Flight Database", "Amazon RDS", "Stores flight booking and availability data")
    }
}

Deployment_Node(storage, "Storage Tier", "Global") {
    Deployment_Node(object_storage, "Object Storage") {
        Container(hotel_images, "Hotel Images", "Amazon S3", "Stores hotel images and related static assets")
        Container(flight_images, "Flight Images", "Amazon S3", "Stores flight images and related static assets")
    }
}

Deployment_Node(monitoring, "Monitoring and Security") {
    Container(logging, "Logging", "AWS CloudWatch", "Captures application logs for debugging and monitoring")
    Container(metrics, "Metrics", "Prometheus/Grafana", "Monitors system performance and usage")
    Container(security, "Web Application Firewall (WAF)", "AWS WAF", "Protects against malicious requests")
}

Rel(web, api_gateway, "Sends requests", "HTTPS")
Rel(app, api_gateway, "Sends requests", "HTTPS")
Rel(api_gateway, auth_service, "Authenticates users", "OAuth2")
Rel(api_gateway, booking_service, "Manages bookings", "REST")
Rel(booking_service, booking_db, "Reads/Writes booking data", "SQL")
Rel(booking_service, user_db, "Reads/Writes user data", "SQL")
Rel(flight_service, flight_db, "Reads/Writes flight data", "SQL")
Rel(notification_service, booking_db, "Fetches booking data", "SQL")
Rel(notification_service, user_db, "Fetches user data", "SQL")
Rel(notification_service, client, "Sends notifications", "SMTP")
Rel(booking_service, flight_service, "Fetches flight details", "API")
Rel(hotel_images, web, "Delivers hotel images", "HTTPS")
Rel(flight_images, app, "Delivers flight images", "HTTPS")

' Non-Functional Requirements (NFRs)
note right of api_gateway
  - Scalability: Auto-scaling based on load
  - High availability: Deployed across multiple availability zones
  - Load balancing: Ensures even distribution of traffic
  - Caching: Use of CloudFront and API Gateway caching for faster responses
end note

note right of api_cluster
  - Performance Monitoring: Prometheus and Grafana
  - Reliability: 99.9% uptime
  - Security: End-to-end encryption (TLS), Data encrypted at rest
  - Auto-scaling: Based on traffic demand
end note

note right of databases
  - Data Redundancy: Multi-Region Replication
  - Backups: Automated backups every 24 hours
  - Security: Role-based access control, Encryption at rest
  - High availability: Failover support
end note

note right of storage
  - Data Redundancy: S3 Cross-Region Replication
  - Security: AES-256 Encryption for stored files
  - Performance: Content Delivery Network (CDN) for fast access to assets
end note

note right of monitoring
  - Centralized Logging: CloudWatch for unified logs
  - Security Monitoring: AWS WAF for threat detection
  - Incident Response: Automated alerts for security breaches and performance degradation
end note
@enduml
```
---
### Key Non-Functional Requirements (NFRs) in the Deployment Diagram:

- **Scalability**: Horizontal scaling enabled by auto-scaling groups for API Gateway and services like Booking Service and Flight Service. Load balancing ensures high performance under varying traffic loads.
- **Availability**: Multi-availability zone deployments across services like API Gateway and databases to ensure high availability and fault tolerance.
- **Caching**: Caching implemented at the API Gateway level with AWS CloudFront for better response times and reduced load on back-end services.
- **Security**: Secure communications using TLS, with encryption of sensitive data at rest in databases and object storage. The Web Application Firewall (WAF) prevents malicious requests.
- **Performance Monitoring**: The system uses Prometheus and Grafana for continuous monitoring of system performance. AWS CloudWatch captures logs for real-time diagnostics.
- **Reliability**: The system guarantees 99.9% uptime with automated backups, failover mechanisms, and high availability configurations for databases and storage.
- **Incident Response**: Automated alerts are set up for any security incidents or system performance degradation, enabling proactive handling of potential issues.
