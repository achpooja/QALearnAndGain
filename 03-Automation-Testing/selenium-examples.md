# Selenium Automation Examples

This directory contains practical Selenium automation examples using Python.

## Prerequisites

```bash
pip install selenium pytest
```

Also download ChromeDriver or use webdriver-manager:
```bash
pip install webdriver-manager
```

## Example 1: Basic Web Automation

### basic_test.py
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
import time

# Setup Chrome driver
driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))

try:
    # Navigate to a website
    driver.get("https://www.saucedemo.com/")
    driver.maximize_window()
    
    # Find elements and interact
    username = driver.find_element(By.ID, "user-name")
    password = driver.find_element(By.ID, "password")
    login_button = driver.find_element(By.ID, "login-button")
    
    # Enter credentials
    username.send_keys("standard_user")
    password.send_keys("secret_sauce")
    
    # Click login
    login_button.click()
    
    # Wait and verify
    time.sleep(2)
    
    # Check if login was successful
    assert "inventory.html" in driver.current_url
    print("Login successful!")
    
finally:
    # Close browser
    driver.quit()
```

## Example 2: Using Explicit Waits

### explicit_wait_example.py
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
wait = WebDriverWait(driver, 10)

try:
    driver.get("https://the-internet.herokuapp.com/dynamic_loading/1")
    
    # Click start button
    start_button = driver.find_element(By.CSS_SELECTOR, "#start button")
    start_button.click()
    
    # Wait for the element to be visible (explicit wait)
    finish_text = wait.until(
        EC.visibility_of_element_located((By.ID, "finish"))
    )
    
    # Verify text
    assert finish_text.text == "Hello World!"
    print("Text appeared successfully!")
    
finally:
    driver.quit()
```

## Example 3: Page Object Model

### pages/login_page.py
```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class LoginPage:
    # Locators
    USERNAME_INPUT = (By.ID, "user-name")
    PASSWORD_INPUT = (By.ID, "password")
    LOGIN_BUTTON = (By.ID, "login-button")
    ERROR_MESSAGE = (By.CSS_SELECTOR, "h3[data-test='error']")
    
    def __init__(self, driver):
        self.driver = driver
        self.wait = WebDriverWait(driver, 10)
    
    def enter_username(self, username):
        """Enter username in the username field"""
        element = self.wait.until(
            EC.visibility_of_element_located(self.USERNAME_INPUT)
        )
        element.clear()
        element.send_keys(username)
    
    def enter_password(self, password):
        """Enter password in the password field"""
        element = self.wait.until(
            EC.visibility_of_element_located(self.PASSWORD_INPUT)
        )
        element.clear()
        element.send_keys(password)
    
    def click_login(self):
        """Click the login button"""
        element = self.wait.until(
            EC.element_to_be_clickable(self.LOGIN_BUTTON)
        )
        element.click()
    
    def login(self, username, password):
        """Complete login process"""
        self.enter_username(username)
        self.enter_password(password)
        self.click_login()
    
    def get_error_message(self):
        """Get error message text"""
        element = self.wait.until(
            EC.visibility_of_element_located(self.ERROR_MESSAGE)
        )
        return element.text
```

### pages/products_page.py
```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class ProductsPage:
    # Locators
    PRODUCTS_TITLE = (By.CLASS_NAME, "title")
    INVENTORY_ITEMS = (By.CLASS_NAME, "inventory_item")
    ADD_TO_CART_BUTTONS = (By.CSS_SELECTOR, "button[class*='btn_inventory']")
    CART_BADGE = (By.CLASS_NAME, "shopping_cart_badge")
    
    def __init__(self, driver):
        self.driver = driver
        self.wait = WebDriverWait(driver, 10)
    
    def is_loaded(self):
        """Check if products page is loaded"""
        try:
            self.wait.until(
                EC.visibility_of_element_located(self.PRODUCTS_TITLE)
            )
            return True
        except:
            return False
    
    def get_products_count(self):
        """Get number of products displayed"""
        elements = self.driver.find_elements(*self.INVENTORY_ITEMS)
        return len(elements)
    
    def add_first_product_to_cart(self):
        """Add the first product to cart"""
        button = self.wait.until(
            EC.element_to_be_clickable(self.ADD_TO_CART_BUTTONS)
        )
        button.click()
    
    def get_cart_items_count(self):
        """Get number of items in cart"""
        try:
            badge = self.driver.find_element(*self.CART_BADGE)
            return int(badge.text)
        except:
            return 0
```

### tests/test_login.py
```python
import pytest
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from pages.login_page import LoginPage
from pages.products_page import ProductsPage

@pytest.fixture
def driver():
    """Setup and teardown for browser"""
    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
    driver.maximize_window()
    yield driver
    driver.quit()

def test_successful_login(driver):
    """Test login with valid credentials"""
    driver.get("https://www.saucedemo.com/")
    
    login_page = LoginPage(driver)
    login_page.login("standard_user", "secret_sauce")
    
    products_page = ProductsPage(driver)
    assert products_page.is_loaded(), "Products page did not load"

def test_invalid_login(driver):
    """Test login with invalid credentials"""
    driver.get("https://www.saucedemo.com/")
    
    login_page = LoginPage(driver)
    login_page.login("invalid_user", "wrong_password")
    
    error_message = login_page.get_error_message()
    assert "Username and password do not match" in error_message

def test_add_product_to_cart(driver):
    """Test adding a product to cart"""
    driver.get("https://www.saucedemo.com/")
    
    # Login first
    login_page = LoginPage(driver)
    login_page.login("standard_user", "secret_sauce")
    
    # Add product to cart
    products_page = ProductsPage(driver)
    assert products_page.is_loaded()
    
    initial_count = products_page.get_cart_items_count()
    products_page.add_first_product_to_cart()
    
    new_count = products_page.get_cart_items_count()
    assert new_count == initial_count + 1, "Product was not added to cart"
```

## Example 4: Data-Driven Testing

### test_data_driven.py
```python
import pytest
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from pages.login_page import LoginPage

@pytest.fixture
def driver():
    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
    driver.maximize_window()
    driver.get("https://www.saucedemo.com/")
    yield driver
    driver.quit()

# Test data
invalid_credentials = [
    ("", "", "Username is required"),
    ("user", "", "Password is required"),
    ("", "pass", "Username is required"),
    ("locked_out_user", "secret_sauce", "locked out"),
]

@pytest.mark.parametrize("username,password,expected_error", invalid_credentials)
def test_invalid_login_scenarios(driver, username, password, expected_error):
    """Test various invalid login scenarios"""
    login_page = LoginPage(driver)
    login_page.login(username, password)
    
    error_message = login_page.get_error_message()
    assert expected_error.lower() in error_message.lower()
```

## Example 5: Handling Different Elements

### element_interactions.py
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))

try:
    # Handling Dropdowns
    driver.get("https://the-internet.herokuapp.com/dropdown")
    dropdown = Select(driver.find_element(By.ID, "dropdown"))
    dropdown.select_by_visible_text("Option 1")
    
    # Handling Checkboxes
    driver.get("https://the-internet.herokuapp.com/checkboxes")
    checkboxes = driver.find_elements(By.CSS_SELECTOR, "input[type='checkbox']")
    for checkbox in checkboxes:
        if not checkbox.is_selected():
            checkbox.click()
    
    # Handling Alerts
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    alert_button = driver.find_element(By.CSS_SELECTOR, "button[onclick='jsAlert()']")
    alert_button.click()
    
    alert = driver.switch_to.alert
    print(f"Alert text: {alert.text}")
    alert.accept()
    
finally:
    driver.quit()
```

## Running the Tests

### Run all tests
```bash
pytest tests/
```

### Run specific test file
```bash
pytest tests/test_login.py
```

### Run with verbose output
```bash
pytest tests/ -v
```

### Run with HTML report
```bash
pip install pytest-html
pytest tests/ --html=report.html
```

## Configuration File

### conftest.py
```python
import pytest
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

@pytest.fixture(scope="function")
def driver():
    """Setup Chrome driver for each test"""
    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
    driver.maximize_window()
    driver.implicitly_wait(10)
    yield driver
    driver.quit()

@pytest.fixture(scope="session")
def base_url():
    """Base URL for the application"""
    return "https://www.saucedemo.com/"
```

## Best Practices Applied

1. **Page Object Model**: Separation of test logic and page elements
2. **Explicit Waits**: Better synchronization
3. **Fixtures**: Reusable setup and teardown
4. **Parametrization**: Data-driven testing
5. **Clean Code**: Descriptive names and comments
6. **Error Handling**: Try-finally blocks
7. **Assertions**: Clear validation messages

## Next Steps

1. Add more complex test scenarios
2. Implement screenshot on failure
3. Add logging
4. Integrate with CI/CD
5. Add API testing alongside UI tests
