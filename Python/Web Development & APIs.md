# Python Web & API Cheat Sheet

### 1. Requests (Working with APIs)
```python
import requests

# GET Request
response = requests.get("https://api.example.com")
if response.status_code == 200:
    data = response.json()  # Parse JSON response

# POST Request with Data
payload = {'key': 'value'}
requests.post("https://api.example.com", json=payload)
```

### 2. Web Scraping (BeautifulSoup)
```python
from bs4 import BeautifulSoup
import requests

url = "https://example.com"
page = requests.get(url)
soup = BeautifulSoup(page.content, 'html.parser')

# Find elements
title = soup.find('h1').text
links = soup.find_all('a')
for link in links:
    print(link.get('href'))
```

### 3. Selenium (Dynamic Content)
```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://example.com")

# Interaction
button = driver.find_element(By.ID, "submit-button")
button.click()
driver.quit()
```
