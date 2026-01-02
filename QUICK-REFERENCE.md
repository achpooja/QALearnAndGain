# QA Quick Reference Guide

## Test Case Writing Template

```
Test Case ID: TC_[MODULE]_[NUMBER]
Title: [Brief description]
Priority: [High/Medium/Low]
Preconditions: [What must be true before testing]
Test Steps:
  1. [Action]
  2. [Action]
  3. [Action]
Expected Result: [What should happen]
Test Data: [Any specific data needed]
```

## Bug Report Template

```
Bug ID: BUG_[NUMBER]
Summary: [One-line description]
Severity: [Critical/High/Medium/Low]
Priority: [Immediate/High/Medium/Low]
Environment: [Browser, OS, version]
Steps to Reproduce:
  1. [Step]
  2. [Step]
  3. [Step]
Expected Result: [What should happen]
Actual Result: [What actually happened]
Attachments: [Screenshots, logs]
```

## Common Test Scenarios

### Login Testing
- Valid credentials
- Invalid username
- Invalid password
- Empty fields
- SQL injection attempts
- Remember me functionality
- Forgot password
- Session timeout
- Multiple login attempts

### Form Testing
- Valid data in all fields
- Invalid data types
- Required field validation
- Field length limits
- Special characters
- Submit button
- Reset/Clear button
- Tab order navigation
- Copy-paste functionality

### E-commerce Testing
- Browse products
- Search functionality
- Add to cart
- Update quantity
- Remove from cart
- Apply discount codes
- Checkout process
- Payment processing
- Order confirmation

## Selenium Quick Commands

### Finding Elements
```python
# By ID
element = driver.find_element(By.ID, "element_id")

# By Name
element = driver.find_element(By.NAME, "element_name")

# By Class Name
element = driver.find_element(By.CLASS_NAME, "class_name")

# By CSS Selector
element = driver.find_element(By.CSS_SELECTOR, "css_selector")

# By XPath
element = driver.find_element(By.XPATH, "//xpath")

# By Link Text
element = driver.find_element(By.LINK_TEXT, "link_text")

# By Partial Link Text
element = driver.find_element(By.PARTIAL_LINK_TEXT, "partial_link")
```

### Common Actions
```python
# Click
element.click()

# Send keys (type)
element.send_keys("text")

# Clear field
element.clear()

# Get text
text = element.text

# Get attribute
value = element.get_attribute("value")

# Is displayed
is_visible = element.is_displayed()

# Is enabled
is_enabled = element.is_enabled()

# Is selected (for checkboxes/radio)
is_selected = element.is_selected()
```

### Waits
```python
# Implicit Wait (applies to all elements)
driver.implicitly_wait(10)

# Explicit Wait
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(
    EC.presence_of_element_located((By.ID, "element_id"))
)

# Common Expected Conditions
EC.presence_of_element_located()
EC.visibility_of_element_located()
EC.element_to_be_clickable()
EC.text_to_be_present_in_element()
EC.alert_is_present()
```

### Navigation
```python
# Navigate to URL
driver.get("https://example.com")

# Go back
driver.back()

# Go forward
driver.forward()

# Refresh
driver.refresh()

# Get current URL
current_url = driver.current_url

# Get page title
title = driver.title
```

## API Testing Quick Reference

### HTTP Methods
- **GET**: Retrieve data
- **POST**: Create new resource
- **PUT**: Update entire resource
- **PATCH**: Update partial resource
- **DELETE**: Remove resource

### HTTP Status Codes
- **200 OK**: Successful GET, PUT, PATCH
- **201 Created**: Successful POST
- **204 No Content**: Successful DELETE
- **400 Bad Request**: Invalid request
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: No permission
- **404 Not Found**: Resource doesn't exist
- **500 Internal Server Error**: Server error

### Python Requests Example
```python
import requests

# GET request
response = requests.get("https://api.example.com/users/1")
assert response.status_code == 200
data = response.json()

# POST request
payload = {"name": "Test", "email": "test@example.com"}
response = requests.post("https://api.example.com/users", json=payload)
assert response.status_code == 201

# PUT request
payload = {"name": "Updated Name"}
response = requests.put("https://api.example.com/users/1", json=payload)

# DELETE request
response = requests.delete("https://api.example.com/users/1")
assert response.status_code == 204
```

## Testing Checklist

### Pre-Testing
- [ ] Understand requirements
- [ ] Review acceptance criteria
- [ ] Identify test scenarios
- [ ] Prepare test data
- [ ] Set up test environment

### During Testing
- [ ] Execute test cases
- [ ] Document results
- [ ] Report bugs
- [ ] Retest fixed bugs
- [ ] Update test cases

### Post-Testing
- [ ] Test summary report
- [ ] Metrics collection
- [ ] Lessons learned
- [ ] Update documentation

## Common XPath Patterns

```xpath
// Select by ID
//*[@id='element_id']

// Select by class
//*[@class='class_name']

// Select by attribute
//*[@name='attribute_value']

// Select by text
//*[text()='exact_text']

// Contains text
//*[contains(text(), 'partial_text')]

// Starts with
//*[starts-with(@id, 'prefix')]

// Parent
//element/..

// Following sibling
//element/following-sibling::div

// Preceding sibling
//element/preceding-sibling::div

// Child
//parent/child

// Descendant
//ancestor//descendant
```

## Regular Expressions for Validation

```regex
Email: ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$

Phone (US): ^\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$

URL (basic): ^https?://[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}(/.*)?$
Note: This is a simplified version for basic validation

ZIP Code (US): ^\d{5}(-\d{4})?$

Credit Card (Visa/Mastercard only): ^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14})$
Note: Add patterns for Amex (^3[47][0-9]{13}$) and other cards as needed

Date (YYYY-MM-DD): ^\d{4}-\d{2}-\d{2}$

Password (8+ chars, 1 upper, 1 lower, 1 number):
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$
```

## Git Commands for Testers

```bash
# Clone repository
git clone <repository_url>

# Check status
git status

# Create new branch
git checkout -b feature/test-automation

# Add files
git add .

# Commit changes
git commit -m "Add test cases for login"

# Push to remote
git push origin branch_name

# Pull latest changes
git pull origin main

# View commit history
git log --oneline

# Discard local changes
git checkout -- <file>
```

## Performance Testing Metrics

- **Response Time**: Time taken to receive a response
- **Throughput**: Number of requests processed per unit time
- **Error Rate**: Percentage of failed requests
- **CPU Usage**: Processor utilization percentage
- **Memory Usage**: RAM utilization
- **Network I/O**: Data transfer rate
- **Concurrent Users**: Number of simultaneous users

## Test Pyramid

```
     /\
    /UI\      <- Few (10%)
   /----\
  /  API \    <- More (30%)
 /--------\
/ Unit     \  <- Most (60%)
------------
```

## Testing Types Quick List

**Functional Testing**
- Unit Testing
- Integration Testing
- System Testing
- Acceptance Testing
- Smoke Testing
- Sanity Testing
- Regression Testing

**Non-Functional Testing**
- Performance Testing
- Load Testing
- Stress Testing
- Security Testing
- Usability Testing
- Compatibility Testing
- Reliability Testing

## Keyboard Shortcuts for DevTools

**Chrome DevTools**
- F12 or Ctrl+Shift+I: Open DevTools
- Ctrl+Shift+C: Inspect element
- Ctrl+Shift+J: Open Console
- Ctrl+Shift+M: Toggle device toolbar
- Ctrl+]: Next panel
- Ctrl+[: Previous panel
- Ctrl+F: Search in current file

## SQL Injection Test Strings

```sql
' OR '1'='1
' OR 1=1--
admin'--
' OR 'x'='x
1' OR '1'='1
```

*Note: Only test on systems you're authorized to test!*

## XSS Test Strings

```html
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg/onload=alert('XSS')>
javascript:alert('XSS')
```

*Note: Only test on systems you're authorized to test!*

## Remember

✅ **DO:**
- Test early and often
- Report bugs clearly
- Document your tests
- Collaborate with developers
- Keep learning

❌ **DON'T:**
- Test in production without permission
- Assume anything works
- Skip regression testing
- Ignore edge cases
- Stop learning
