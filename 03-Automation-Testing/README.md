# Automation Testing

## Introduction to Test Automation

Test automation is the practice of running tests automatically, managing test data, and utilizing results to improve software quality. It's essential for continuous integration and continuous delivery (CI/CD).

## When to Automate

### Good Candidates for Automation
- **Regression tests**: Tests that run frequently
- **Smoke tests**: Quick sanity checks
- **Data-driven tests**: Same test with different data sets
- **Repetitive tests**: Tests that are tedious to perform manually
- **Performance tests**: Load, stress, and scalability tests

### Poor Candidates for Automation
- **One-time tests**: Won't be run again
- **Exploratory tests**: Require human judgment
- **UI tests that change frequently**: High maintenance cost
- **Complex user experience tests**: Hard to automate effectively

## Automation Testing Types

### 1. Unit Testing
- Test individual functions or methods
- Fast and isolated
- Usually written by developers

### 2. Integration Testing
- Test interactions between components
- Verify APIs and services work together

### 3. UI/E2E Testing
- Test from user's perspective
- Verify complete workflows
- Most expensive to maintain

### 4. API Testing
- Test backend services
- Fast and reliable
- Independent of UI changes

## Popular Automation Tools

### Web Testing
- **Selenium**: Browser automation framework
- **Cypress**: Modern JavaScript testing
- **Playwright**: Cross-browser automation
- **Puppeteer**: Chrome/Chromium automation

### Mobile Testing
- **Appium**: Cross-platform mobile testing
- **Espresso**: Android native testing
- **XCUITest**: iOS native testing

### API Testing
- **Postman**: API testing platform
- **REST Assured**: Java library for REST APIs
- **SoapUI**: SOAP and REST testing

### Unit Testing
- **JUnit**: Java unit testing
- **pytest**: Python testing framework
- **Jest**: JavaScript testing framework
- **NUnit**: .NET testing framework

## Automation Best Practices

### 1. Test Pyramid
```
        /\
       /E2E\       Few UI tests (slow, expensive)
      /______\
     /        \
    / Integration\  More integration tests
   /______________\
  /                \
 /   Unit Tests     \  Many unit tests (fast, cheap)
/____________________\
```

### 2. Writing Maintainable Tests
- **Use Page Object Model (POM)**: Separate test logic from page structure
- **Keep tests independent**: Each test should run standalone
- **Use descriptive names**: Test names should explain what they test
- **Avoid hard-coded waits**: Use explicit waits instead
- **Keep tests simple**: One test should verify one thing

### 3. Test Data Management
- Use test data factories
- Clean up data after tests
- Use unique data for each test run
- Separate test data from test code

## Selenium Example (Python)

### Basic Test Structure
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class TestLogin:
    def setup_method(self):
        self.driver = webdriver.Chrome()
        self.driver.get("https://example.com/login")
    
    def test_valid_login(self):
        # Find elements
        username = self.driver.find_element(By.ID, "username")
        password = self.driver.find_element(By.ID, "password")
        login_btn = self.driver.find_element(By.ID, "login")
        
        # Enter credentials
        username.send_keys("testuser")
        password.send_keys("testpass")
        login_btn.click()
        
        # Wait for success message
        wait = WebDriverWait(self.driver, 10)
        success = wait.until(
            EC.presence_of_element_located((By.CLASS_NAME, "success"))
        )
        
        # Verify
        assert "Welcome" in success.text
    
    def teardown_method(self):
        self.driver.quit()
```

### Page Object Model Example
```python
class LoginPage:
    def __init__(self, driver):
        self.driver = driver
        self.username_input = (By.ID, "username")
        self.password_input = (By.ID, "password")
        self.login_button = (By.ID, "login")
    
    def login(self, username, password):
        self.driver.find_element(*self.username_input).send_keys(username)
        self.driver.find_element(*self.password_input).send_keys(password)
        self.driver.find_element(*self.login_button).click()

class TestLogin:
    def test_valid_login(self):
        login_page = LoginPage(self.driver)
        login_page.login("testuser", "testpass")
        # Add assertions
```

## API Testing Example

### Using Python Requests
```python
import requests
import pytest

class TestUserAPI:
    BASE_URL = "https://api.example.com"
    
    def test_get_user(self):
        response = requests.get(f"{self.BASE_URL}/users/1")
        
        assert response.status_code == 200
        data = response.json()
        assert "id" in data
        assert "name" in data
        assert data["id"] == 1
    
    def test_create_user(self):
        payload = {
            "name": "Test User",
            "email": "test@example.com"
        }
        response = requests.post(f"{self.BASE_URL}/users", json=payload)
        
        assert response.status_code == 201
        data = response.json()
        assert data["name"] == payload["name"]
        assert "id" in data
```

## CI/CD Integration

### GitHub Actions Example
```yaml
name: Automated Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.9
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest tests/
```

## Exercises

1. **Set up a simple Selenium test**
   - Install Selenium and a web driver
   - Write a test to navigate to a website
   - Find an element and verify its text

2. **Create an API test**
   - Use a public API (like JSONPlaceholder)
   - Write tests for GET, POST, PUT, DELETE
   - Add assertions for status codes and response data

3. **Implement Page Object Model**
   - Take an existing test
   - Refactor it using POM pattern
   - Add at least 2 more tests using the same page objects
