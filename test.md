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