# Manual Testing

## Introduction to Manual Testing

Manual testing is the process of manually testing software for defects. It requires a tester to play the role of an end user and use most of the application's features to ensure correct behavior.

## When to Use Manual Testing

- **Exploratory Testing**: When you need human insight
- **Usability Testing**: Evaluating user experience
- **Ad-hoc Testing**: Quick, informal testing
- **First-time Testing**: When automating isn't cost-effective yet

## Manual Testing Techniques

### 1. Exploratory Testing
- Learn, design, and execute tests simultaneously
- Rely on tester's creativity and experience
- No predefined test cases

### 2. Ad-hoc Testing
- Informal testing without documentation
- Random testing based on tester's knowledge
- Good for finding unusual bugs

### 3. Scripted Testing
- Follow predefined test cases
- Systematic and repeatable
- Good for regression testing

## Writing Effective Test Cases

### Test Case Components
```
Test Case ID: TC_001
Test Case Title: Verify login with valid credentials
Preconditions: User is registered in the system
Test Steps:
  1. Navigate to login page
  2. Enter valid username
  3. Enter valid password
  4. Click login button
Expected Result: User is logged in successfully
Actual Result: [To be filled during execution]
Status: [Pass/Fail]
```

### Best Practices for Test Cases
- **Clear and Concise**: Easy to understand and execute
- **Reusable**: Can be used across different test cycles
- **Traceable**: Linked to requirements
- **Independent**: Can be executed in any order
- **Maintainable**: Easy to update when requirements change

## Test Case Examples

### Example 1: Login Functionality
```
Test Scenario: User Login
Test Case 1: Valid login
Test Case 2: Invalid username
Test Case 3: Invalid password
Test Case 4: Empty credentials
Test Case 5: SQL injection attempt
```

### Example 2: Shopping Cart
```
Test Scenario: Add to Cart
Test Case 1: Add single item
Test Case 2: Add multiple items
Test Case 3: Add out of stock item
Test Case 4: Remove item from cart
Test Case 5: Update quantity
```

## Bug Reporting

### Bug Report Template
```
Bug ID: BUG_001
Summary: Login button not working
Description: When clicking the login button, nothing happens
Steps to Reproduce:
  1. Navigate to login page
  2. Enter credentials
  3. Click login button
Expected Result: User should be logged in
Actual Result: Nothing happens
Severity: High
Priority: High
Environment: Chrome 95.0, Windows 10
Attachments: [Screenshots/Videos]
```

### Severity vs Priority
- **Severity**: Impact of the bug (Critical, High, Medium, Low)
- **Priority**: Urgency to fix (Immediate, High, Medium, Low)

## Testing Checklists

### Login Page Testing Checklist
- [ ] Valid credentials login
- [ ] Invalid username
- [ ] Invalid password
- [ ] Empty fields
- [ ] Remember me functionality
- [ ] Forgot password link
- [ ] Field validation
- [ ] Password masking
- [ ] Case sensitivity
- [ ] SQL injection
- [ ] XSS attacks
- [ ] Session timeout
- [ ] Logout functionality

### Form Testing Checklist
- [ ] All fields accept valid data
- [ ] Required field validation
- [ ] Data type validation
- [ ] Field length validation
- [ ] Special character handling
- [ ] Submit button functionality
- [ ] Reset button functionality
- [ ] Error messages display
- [ ] Success messages display

## Practical Exercise

Create test cases for the following scenarios:

1. **User Registration Form**
   - Fields: Username, Email, Password, Confirm Password
   - Write at least 10 test cases

2. **Search Functionality**
   - Test with valid search terms
   - Test with invalid search terms
   - Test with special characters
   - Test empty search

3. **E-commerce Checkout**
   - Add items to cart
   - Apply discount code
   - Select shipping method
   - Enter payment details
   - Complete purchase
