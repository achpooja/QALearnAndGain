# Sample Test Cases

## Test Case Template

```
Test Case ID: TC_XXX
Module: [Module Name]
Test Case Title: [Brief description]
Preconditions: [What must be true before executing]
Test Steps:
  1. [Step 1]
  2. [Step 2]
  3. [Step 3]
Expected Result: [What should happen]
Actual Result: [To be filled during execution]
Status: [Pass/Fail/Blocked/N/A]
Priority: [High/Medium/Low]
Test Data: [Any specific data needed]
```

## Login Functionality Test Cases

### TC_LOGIN_001: Verify login with valid credentials
```
Test Case ID: TC_LOGIN_001
Module: Authentication
Test Case Title: Verify login with valid credentials
Preconditions: 
  - User is registered with username "testuser" and password "Test@123"
  - User is on login page
Test Steps:
  1. Enter valid username "testuser"
  2. Enter valid password "Test@123"
  3. Click on "Login" button
Expected Result: 
  - User is redirected to dashboard
  - Welcome message is displayed
  - User session is created
Status: [To be executed]
Priority: High
Test Data: Username: testuser, Password: Test@123
```

### TC_LOGIN_002: Verify login with invalid username
```
Test Case ID: TC_LOGIN_002
Module: Authentication
Test Case Title: Verify login with invalid username
Preconditions: User is on login page
Test Steps:
  1. Enter invalid username "invaliduser"
  2. Enter valid password "Test@123"
  3. Click on "Login" button
Expected Result: 
  - Error message "Invalid credentials" is displayed
  - User remains on login page
  - Login attempt is logged
Status: [To be executed]
Priority: High
Test Data: Username: invaliduser, Password: Test@123
```

### TC_LOGIN_003: Verify login with invalid password
```
Test Case ID: TC_LOGIN_003
Module: Authentication
Test Case Title: Verify login with invalid password
Preconditions: User is on login page
Test Steps:
  1. Enter valid username "testuser"
  2. Enter invalid password "wrongpass"
  3. Click on "Login" button
Expected Result: 
  - Error message "Invalid credentials" is displayed
  - User remains on login page
  - Failed login attempt is logged
Status: [To be executed]
Priority: High
Test Data: Username: testuser, Password: wrongpass
```

### TC_LOGIN_004: Verify login with empty credentials
```
Test Case ID: TC_LOGIN_004
Module: Authentication
Test Case Title: Verify login with empty credentials
Preconditions: User is on login page
Test Steps:
  1. Leave username field empty
  2. Leave password field empty
  3. Click on "Login" button
Expected Result: 
  - Validation error "Username is required" is displayed
  - Validation error "Password is required" is displayed
  - Login button remains inactive or shows validation
Status: [To be executed]
Priority: Medium
Test Data: Username: [empty], Password: [empty]
```

### TC_LOGIN_005: Verify password masking
```
Test Case ID: TC_LOGIN_005
Module: Authentication
Test Case Title: Verify password masking
Preconditions: User is on login page
Test Steps:
  1. Enter any text in password field
  2. Observe the password field
Expected Result: 
  - Password characters are masked (shown as dots or asterisks)
  - Actual password is not visible
Status: [To be executed]
Priority: Medium
Test Data: Password: anypassword123
```

## E-commerce Test Cases

### TC_CART_001: Add single item to cart
```
Test Case ID: TC_CART_001
Module: Shopping Cart
Test Case Title: Add single item to cart
Preconditions: 
  - User is logged in
  - At least one product is available
Test Steps:
  1. Navigate to product page
  2. Click "Add to Cart" button
  3. Navigate to cart page
Expected Result: 
  - Product appears in cart
  - Cart count increases by 1
  - Total price is updated correctly
Status: [To be executed]
Priority: High
Test Data: Product ID: PROD_001
```

### TC_CART_002: Update item quantity in cart
```
Test Case ID: TC_CART_002
Module: Shopping Cart
Test Case Title: Update item quantity in cart
Preconditions: 
  - User is logged in
  - Cart has at least one item
Test Steps:
  1. Navigate to cart page
  2. Change quantity to 3
  3. Click "Update" button
Expected Result: 
  - Quantity is updated to 3
  - Total price reflects new quantity
  - Success message is displayed
Status: [To be executed]
Priority: High
Test Data: Initial quantity: 1, New quantity: 3
```

### TC_CART_003: Remove item from cart
```
Test Case ID: TC_CART_003
Module: Shopping Cart
Test Case Title: Remove item from cart
Preconditions: 
  - User is logged in
  - Cart has at least one item
Test Steps:
  1. Navigate to cart page
  2. Click "Remove" button for an item
  3. Confirm removal if prompted
Expected Result: 
  - Item is removed from cart
  - Cart count decreases
  - Total price is updated
  - "Item removed" message is displayed
Status: [To be executed]
Priority: High
Test Data: Product to remove: PROD_001
```

## Form Validation Test Cases

### TC_FORM_001: Verify email field validation
```
Test Case ID: TC_FORM_001
Module: Registration Form
Test Case Title: Verify email field validation
Preconditions: User is on registration page
Test Steps:
  1. Enter invalid email "notanemail"
  2. Click on submit button
Expected Result: 
  - Error message "Please enter a valid email" is displayed
  - Form is not submitted
Status: [To be executed]
Priority: High
Test Data: Email: notanemail
```

### TC_FORM_002: Verify password strength requirements
```
Test Case ID: TC_FORM_002
Module: Registration Form
Test Case Title: Verify password strength requirements
Preconditions: User is on registration page
Test Steps:
  1. Enter weak password "123"
  2. Tab to next field or click submit
Expected Result: 
  - Error message "Password must be at least 8 characters" is displayed
  - Password strength indicator shows "Weak"
  - Form is not submitted
Status: [To be executed]
Priority: High
Test Data: Password: 123
```

### TC_FORM_003: Verify required field validation
```
Test Case ID: TC_FORM_003
Module: Contact Form
Test Case Title: Verify required field validation
Preconditions: User is on contact form page
Test Steps:
  1. Leave all required fields empty
  2. Click "Submit" button
Expected Result: 
  - All required fields show validation errors
  - Error messages are clear and specific
  - Form is not submitted
Status: [To be executed]
Priority: High
Test Data: All fields: [empty]
```

## Search Functionality Test Cases

### TC_SEARCH_001: Search with valid keyword
```
Test Case ID: TC_SEARCH_001
Module: Search
Test Case Title: Search with valid keyword
Preconditions: Database has products matching "laptop"
Test Steps:
  1. Enter "laptop" in search box
  2. Press Enter or click search icon
Expected Result: 
  - Search results page displays
  - Results contain items with "laptop" in title/description
  - Result count is displayed
Status: [To be executed]
Priority: High
Test Data: Keyword: laptop
```

### TC_SEARCH_002: Search with no results
```
Test Case ID: TC_SEARCH_002
Module: Search
Test Case Title: Search with no results
Preconditions: User is on search page
Test Steps:
  1. Enter "xyznonexistent" in search box
  2. Press Enter or click search icon
Expected Result: 
  - "No results found" message is displayed
  - Suggestions or related items may be shown
  - Search page remains functional
Status: [To be executed]
Priority: Medium
Test Data: Keyword: xyznonexistent
```

### TC_SEARCH_003: Search with special characters
```
Test Case ID: TC_SEARCH_003
Module: Search
Test Case Title: Search with special characters
Preconditions: User is on search page
Test Steps:
  1. Enter special characters "!@#$%^&*()" in search box
  2. Press Enter or click search icon
Expected Result: 
  - Application handles special characters gracefully
  - No error/crash occurs
  - Either shows no results or sanitizes input
Status: [To be executed]
Priority: Medium
Test Data: Keyword: !@#$%^&*()
```

## API Test Cases

### TC_API_001: GET request for existing user
```
Test Case ID: TC_API_001
Module: User API
Test Case Title: GET request for existing user
Preconditions: User with ID 1 exists in database
Test Steps:
  1. Send GET request to /api/users/1
  2. Verify response
Expected Result: 
  - Status code: 200 OK
  - Response contains user data
  - Response time < 2 seconds
  - Required fields present: id, name, email
Status: [To be executed]
Priority: High
Test Data: User ID: 1
```

### TC_API_002: POST request to create user
```
Test Case ID: TC_API_002
Module: User API
Test Case Title: POST request to create user
Preconditions: API is accessible
Test Steps:
  1. Send POST request to /api/users with valid payload
  2. Verify response
Expected Result: 
  - Status code: 201 Created
  - Response contains created user with generated ID
  - User is saved in database
Status: [To be executed]
Priority: High
Test Data: 
  {
    "name": "Test User",
    "email": "test@example.com"
  }
```

## Performance Test Scenarios

### TC_PERF_001: Load test with 100 concurrent users
```
Test Case ID: TC_PERF_001
Module: System Performance
Test Case Title: Load test with 100 concurrent users
Preconditions: Application is deployed in test environment
Test Steps:
  1. Configure 100 virtual users
  2. Execute login and browse scenario
  3. Run for 10 minutes
  4. Collect metrics
Expected Result: 
  - Average response time < 3 seconds
  - Error rate < 1%
  - Server CPU < 80%
  - Server memory < 85%
Status: [To be executed]
Priority: High
Test Data: 100 concurrent users, 10 minutes duration
```

## Security Test Cases

### TC_SEC_001: SQL Injection test
```
Test Case ID: TC_SEC_001
Module: Security
Test Case Title: SQL Injection test on login
Preconditions: User is on login page

⚠️ IMPORTANT WARNING ⚠️
This test case is for EDUCATIONAL purposes only.
Only perform security testing on:
- Systems you own
- Systems you have written authorization to test
- Dedicated practice/test environments
Unauthorized testing may be illegal and unethical.

Test Steps:
  1. Enter "admin' OR '1'='1" in username
  2. Enter any password
  3. Click login
Expected Result: 
  - Login is rejected
  - Error message shown
  - No database query is executed
  - Attempt is logged
Status: [To be executed]
Priority: Critical
Test Data: Username: admin' OR '1'='1
```

### TC_SEC_002: XSS attack test
```
Test Case ID: TC_SEC_002
Module: Security
Test Case Title: Cross-Site Scripting test
Preconditions: User is on comment/input form
Test Steps:
  1. Enter "<script>alert('XSS')</script>" in text field
  2. Submit the form
  3. View the submitted content
Expected Result: 
  - Script is not executed
  - Content is sanitized/escaped
  - Raw script tag is not displayed
Status: [To be executed]
Priority: Critical
Test Data: Input: <script>alert('XSS')</script>
```
