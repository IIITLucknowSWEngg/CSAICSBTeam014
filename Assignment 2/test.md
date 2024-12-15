# Test Plan for MakeMyTrip Platform

## 1. User Features

### 1.1 Feature: User - Sign Up  
*Scenario:* User creates a new account  

*Given:*  
- The user is on the MakeMyTrip sign-up page.  

*When:*  
- The user enters valid details (name, email, password, phone number).  
- The user clicks the "Sign Up" button.  

*Then:*  
- The user should be successfully signed up.  
- The user should receive a confirmation email.  
- The user should be redirected to the dashboard.

- *Test Case*:
  - *Code:* 
     ```javascript
     describe('User Sign Up', function() {
        it('should allow user to sign up successfully', function() {
          signUpPage.open();
          signUpPage.enterDetails('John Doe', 'john.doe@example.com', 'password123', '9876543210');
          signUpPage.submitSignUp();
          expect(signUpPage.getConfirmationMessage()).to.include('Account created successfully');
        });
      });
     ```

---

### 1.2 Feature: User - Sign In  
*Scenario:* User logs into their account  

*Given:*  
- The user is on the MakeMyTrip login page.  

*When:*  
- The user enters valid credentials (email and password).  
- The user clicks the "Sign In" button.  

*Then:*  
- The user should be signed in successfully.  
- The user should be redirected to the homepage.

- *Test Case*:
  - *Code:*
    ``` javascript
    describe('User Sign In', function() {
      it('should allow user to sign in successfully with correct credentials', function() {
        loginPage.open();
        loginPage.enterCredentials('john.doe@example.com', 'password123');
        loginPage.submitLogin();
        expect(homePage.getWelcomeMessage()).to.include('Welcome, John Doe');
      });
    });
    ```
---

### 1.3 Feature: User - Search for Flights  
*Scenario:* User searches for flights based on specific criteria  

*Given:*  
- The user is logged in and on the flight search page.  

*When:*  
- The user enters the source and destination city, travel dates, and number of passengers.  
- The user clicks the "Search Flights" button.  

*Then:*  
- The system should return a list of available flights that match the search criteria.  
- The results should be displayed with flight details (airline, price, departure time).

- *Test Case*:
  - *Code:*
    ``` javascript
    describe('User Flight Search', function() {
      it('should show available flights based on search criteria', function() {
        searchPage.open();
        searchPage.enterSearchCriteria('New York', 'Los Angeles', '2023-12-15', 2);
        searchPage.submitSearch();
        expect(searchPage.getSearchResults()).to.be.an('array').that.is.not.empty;
      });
    });
    ```
---

### 1.4 Feature: User - Book Flight  
*Scenario:* User successfully books a flight  

*Given:*  
- The user is logged in and has selected a flight.  

*When:*  
- The user enters passenger details and payment information.  
- The user clicks the "Book Flight" button.  

*Then:*  
- The flight booking should be confirmed.  
- The user should receive a booking confirmation email.  
- The booking details should be available in the user's dashboard.

- *Test Case*:
  - *Code:*
    ``` javascript
     describe('User Flight Booking', function() {
      it('should allow user to book a flight successfully', function() {
        flightDetailsPage.open();
        flightDetailsPage.selectFlight('Flight 101');
        bookingPage.enterPassengerDetails('John Doe', 'john.doe@example.com');
        bookingPage.submitBooking();
        expect(bookingPage.getConfirmationMessage()).to.include('Booking successful');
      });
    });
    ```
---

### 1.5 Feature: User - Cancel Flight Booking  
*Scenario:* User cancels an existing flight booking  

*Given:*  
- The user is logged in and has an existing booking.  

*When:*  
- The user selects a booking and clicks the "Cancel Booking" button.  

*Then:*  
- The booking should be canceled.  
- The user should receive a cancellation confirmation email.  
- The cancellation should be reflected in the user's dashboard.

- *Test Case*:
  - *Code:*
    ``` javascript
    describe('User Cancel Flight Booking', function() {
      it('should allow user to cancel flight booking', function() {
        bookingsPage.open();
        bookingsPage.selectBooking('Flight 101');
        bookingsPage.cancelBooking();
        expect(bookingsPage.getCancellationMessage()).to.include('Booking successfully canceled');
      });
    });
   ```
---

## 2. Admin Features

### 2.1 Feature: Admin - View All Bookings  
*Scenario:* Admin views all user bookings  

*Given:*  
- The admin is logged into the admin portal.  

*When:*  
- The admin navigates to the "Bookings" section.  

*Then:*  
- The admin should be able to see a list of all bookings with details (user name, flight, date, status).

- *Test Case*:
  - *Code:*
   ``` javascript
  describe('Admin View All Bookings', function() {
    it('should allow admin to view all bookings', function() {
       adminDashboard.open();
       adminDashboard.viewBookings();
       const bookings = adminDashboard.getAllBookings();
       expect(bookings).to.be.an('array').that.is.not.empty;
    });
  });
   ```
---

### 2.2 Feature: Admin - Approve/Reject Booking Cancellation  
*Scenario:* Admin approves or rejects a booking cancellation request  

*Given:*  
- The admin is logged into the admin portal.  
- A user has requested a booking cancellation.  

*When:*  
- The admin reviews the request and clicks "Approve" or "Reject."  

*Then:*  
- The cancellation status should be updated accordingly in the system.  
- The user should be notified about the decision.

- *Test Case*:
  - *Code:*
  - ``` javascript
    describe('Admin Approve/Reject Booking Cancellation', function() {
      it('should allow admin to approve or reject booking cancellation request', function() {
        adminDashboard.open();
        adminDashboard.viewCancellationRequest('Flight 101');
        adminDashboard.approveCancellation();
        expect(adminDashboard.getCancellationStatus()).to.include('Approved');
      });
    });
    ```

---

### 2.3 Feature: Admin - Manage Flight Listings  
*Scenario:* Admin adds, updates, or deletes a flight listing  

*Given:*  
- The admin is logged into the admin portal.  

*When:*  
- The admin navigates to the "Flight Listings" section and adds/updates/deletes a flight.  

*Then:*  
- The flight listing should be updated accordingly in the system.  
- The changes should be reflected on the user-facing platform.

- *Test Case*:
  - *Code:*
    ``` javascript
     describe('Admin Manage Flight Listings', function() {
      it('should allow admin to add or delete flight listings', function() {
        adminDashboard.open();
        adminDashboard.addFlight('Flight 102', 'Airline XYZ', '2023-12-20', '11:00 AM');
        expect(adminDashboard.getFlightList()).to.include('Flight 102');
        adminDashboard.deleteFlight('Flight 102');
        expect(adminDashboard.getFlightList()).to.not.include('Flight 102');
      });
    });
  ```
---

## 3. Travel Partner Features

### 3.1 Feature: Travel Partner - Add New Flights  
**Scenario:** Travel partner adds new flights to the system  

**Given:**  
- The travel partner is logged into their partner portal.  

**When:**  
- The travel partner adds new flight details (airline, flight number, schedule, etc.).  

**Then:**  
- The new flight should be added to the flight listings.  
- The new flight should be available for booking by users.

- **Test Case**:
  - **Code:**
    ```javascript
    describe('Travel Partner Add New Flights', function() {
      it('should allow partner to add new flight successfully', function() {
        partnerDashboard.open();
        partnerDashboard.addFlight('Airline ABC', 'Flight 101', '2023-12-15', '10:00 AM', '100');
        expect(partnerDashboard.getFlightList()).to.include('Flight 101');
      });
    });
    ```
---

### 3.2 Feature: Travel Partner - Update Flight Details  
**Scenario:** Travel partner updates flight details  

**Given:**  
- The travel partner is logged into their partner portal.  

**When:**  
- The travel partner updates flight details (schedule, price, etc.).  

**Then:**  
- The updated flight details should be reflected in the system.  
- The updated information should be available for users when searching for flights.

- **Test Case**:
  - **Code:**
    ```javascript
    describe('Travel Partner Update Flight Details', function() {
      it('should allow partner to update flight details successfully', function() {
        partnerDashboard.open();
        partnerDashboard.updateFlight('Flight 101', '2023-12-16', '12:00 PM');
        expect(partnerDashboard.getFlightDetails('Flight 101')).to.include('2023-12-16');
      });
    });
    ```

---

### 3.3 Feature: Travel Partner - View Bookings  
**Scenario:** Travel partner views flight bookings  

**Given:**  
- The travel partner is logged into their partner portal.  

**When:**  
- The travel partner navigates to the "Bookings" section.  

**Then:**  
- The travel partner should see a list of all bookings made for their flights, including user details and booking status.

- **Test Case**:
  - **Code:**
    ```javascript
    describe('Travel Partner View Bookings', function() {
      it('should allow partner to view all bookings made for their flights', function() {
        partnerDashboard.open();
        partnerDashboard.viewBookings();
        const bookings = partnerDashboard.getBookings('Flight 101');
        expect(bookings).to.be.an('array').that.is.not.empty;
      });
    });
    ```

---

## 4. General Features

### 4.1 Feature: User - View Profile  
**Scenario:** User views their profile  

**Given:**  
- The user is logged in.  

**When:**  
- The user navigates to their profile page.  

**Then:**  
- The user's profile details (name, email, phone number) should be visible.

- **Test Case**:
  - **Code:**
    ```javascript
    describe('User View Profile', function() {
      it('should allow user to view profile details', function() {
        userProfilePage.open();
        const profile = userProfilePage.getProfileDetails();
        expect(profile).to.include('John Doe');
        expect(profile).to.include('john.doe@example.com');
      });
    });
    ```

---

### 4.2 Feature: User - Edit Profile  
**Scenario:** User edits their profile  

**Given:**  
- The user is logged in.  

**When:**  
- The user clicks on "Edit Profile" and updates their details (e.g., email, phone number).  

**Then:**  
- The updated details should be saved, and a confirmation message should be shown.

- **Test Case**:
  - **Code:**
    ```javascript
    describe('User Edit Profile', function() {
      it('should allow user to edit profile details', function() {
        userProfilePage.open();
        userProfilePage.editProfile('Jane Doe', 'jane.doe@example.com');
        expect(userProfilePage.getProfileDetails()).to.include('Jane Doe');
        expect(userProfilePage.getProfileDetails()).to.include('jane.doe@example.com');
      });
    });
    ```

---

## 5. Non-Functional Requirements (NFRs)

To ensure the MakeMyTrip platform delivers a high-quality experience, we have outlined test scenarios for the following non-functional requirements: Performance, Usability, Security, Reliability, and Maintainability.

---

### 5.1 Performance

This section evaluates the platform's efficiency and responsiveness under various conditions.

| Test Scenario                             | Description                                                                 | Success Criteria                                                                 | Testing Tools/Methodology                            |
|-------------------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------|-----------------------------------------------------|
| Response time under normal and peak loads | Measure how quickly the platform responds during login, search, and booking.| Response time should be less than 2 seconds for 95% of interactions.           | Use Apache JMeter, Locust for load testing.         |
| Scalability with increased user base      | Simulate up to 10,000 concurrent users to assess the system's scalability.  | The system should handle the load without crashing or significant performance degradation. | Perform stress testing using cloud-based load simulators. |
| Flight search results latency             | Evaluate the time taken to fetch flight search results.                     | Search results should appear within 3 seconds for 95% of queries.              | Implement API response monitoring tools like Postman. |
| Database query performance                | Measure database query execution time during peak operations.               | Queries should execute within 500ms for 90% of transactions.                   | Use tools like New Relic or Dynatrace.              |

---

### 5.2 Usability

This section focuses on user-friendliness and ease of interaction.

| Test Scenario                              | Description                                                                  | Success Criteria                                                            | Testing Tools/Methodology                   |
|--------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------|----------------------------------------------|
| Ease of navigation                         | Assess the intuitiveness of the user interface (UI).                         | Users should be able to navigate to their desired feature in ≤3 clicks.   | Perform heuristic evaluations and A/B testing. |
| Accessibility for differently-abled users  | Ensure compatibility with screen readers and other assistive technologies.   | Compliance with WCAG 2.1 AA standards.                                   | Use WAVE and Axe Accessibility Checker.        |
| Consistent UI and UX                       | Validate that the platform maintains a uniform design and experience across pages. | Users should find the interface consistent and free from visual anomalies. | Conduct user surveys and usability testing.     |
| Mobile responsiveness                      | Test usability on devices of varying screen sizes (mobile, tablet, desktop).  | UI should adapt seamlessly to all screen sizes without breaking.          | Use BrowserStack or LambdaTest.               |

---

### 5.3 Security

This section ensures that the platform protects user data and mitigates potential risks.

| Test Scenario                 | Description                                                                 | Success Criteria                                                                    | Testing Tools/Methodology          |
|-------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------|------------------------------------|
| Data encryption               | Ensure sensitive data (e.g., passwords, payment info) is encrypted at rest and in transit. | All sensitive data should be encrypted using AES-256 or TLS 1.2/1.3.             | Use Wireshark or Burp Suite.       |
| Authentication and authorization | Validate secure login and role-based access control (RBAC).             | Unauthorized users should be unable to access restricted areas.                  | Perform penetration testing with OWASP ZAP. |
| Vulnerability assessment      | Identify and mitigate potential vulnerabilities in the codebase.          | No high-severity vulnerabilities should remain unresolved.                       | Use tools like Nessus or Qualys.   |
| Security against injections   | Test for SQL injection, XSS, and CSRF vulnerabilities.                    | The system should reject malicious payloads and maintain integrity.              | Conduct automated testing with Acunetix. |

---

### 5.4 Reliability

This section assesses the system's dependability under normal and stress conditions.

| Test Scenario                     | Description                                                         | Success Criteria                                                              | Testing Tools/Methodology        |
|-----------------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------|----------------------------------|
| Uptime and availability           | Test the platform's uptime under continuous operations.            | Ensure 99.9% uptime as per SLA.                                              | Use Pingdom or UptimeRobot.      |
| Failure recovery time             | Measure the time to recover from a system failure.                 | Recovery time should not exceed 5 minutes for critical services.             | Perform failover testing.        |
| Data consistency after failures   | Validate the consistency of data after unexpected crashes.         | Data should remain accurate and complete post-recovery.                      | Conduct crash recovery testing.  |
| Error handling                    | Ensure graceful handling of unexpected errors.                     | Users should see informative error messages instead of system crashes.       | Perform fault injection testing. |

---

### 5.5 Maintainability

This section evaluates the platform's ease of maintenance and adaptability to changes.

| Test Scenario                       | Description                                                         | Success Criteria                                                                    | Testing Tools/Methodology       |
|-------------------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------|----------------------------------|
| Code readability and documentation  | Check if the codebase is clean and well-documented.                | Developers should understand and modify code with minimal ramp-up time.           | Perform code reviews and audits. |
| Modular architecture                | Validate that the system follows modular design principles.        | New features should integrate easily without affecting existing modules.          | Analyze system design diagrams.  |
| Dependency updates                  | Test the ability to update external dependencies (e.g., libraries, APIs). | Updates should be applied without breaking functionality.                         | Conduct compatibility testing.   |
| Automated testing coverage          | Ensure robust automated test coverage for critical modules.        | ≥90% of critical functionality should have automated test coverage.               | Use Jest, Mocha, or Selenium.    |

---

## 6. Conclusion

The test plan for the MakeMyTrip platform ensures that all critical functionalities related to user, admin, and travel partner features are thoroughly tested. By covering both positive and negative scenarios, we aim to validate the platform’s stability, usability, and performance. The integration of all features and their seamless execution is essential to provide users with a smooth and efficient experience while interacting with the system.

- **Test Coverage:**  
  - User Sign Up/Sign In
  - Flight Search, Booking, and Cancellation
  - Admin functionalities for managing bookings and flight listings
  - Travel partner flight management
  - General profile management features
  
The test cases defined in this document serve as a solid foundation for identifying issues early in the development lifecycle, ensuring quality and reliability in the final release.

---

