# Web Scraping Learning Project

A collection of web scraping scripts demonstrating various techniques using Selenium and Playwright to extract data from websites.

## 📋 Table of Contents

- [Overview](#overview)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Scripts Description](#scripts-description)
- [Usage Examples](#usage-examples)
- [Key Concepts Learned](#key-concepts-learned)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)

## 🎯 Overview

This project contains practical examples of web scraping techniques, progressing from basic page scraping to handling dynamic content, infinite scroll, and form interactions. All scripts use the practice website [quotes.toscrape.com](http://quotes.toscrape.com) which is designed for learning web scraping.

## 🛠️ Technologies Used

- **Python 3.11+**
- **Selenium** - Browser automation framework
- **Playwright** - Modern web testing and automation
- **BeautifulSoup4** - HTML parsing library
- **ChromeDriver** - WebDriver for Chrome/Brave browsers

## 📁 Project Structure

```
web-scraping-project/
│
├── 1_basic_scraping.py                  # Basic web scraping with Selenium
├── 2_dynamic_content.py                 # Handling dynamic content
├── 3_infinite_scroll_selenium.py        # Infinite scroll with Selenium
├── 4_infinite_scroll_comparison.py      # Comparing scroll implementations
├── 5_form_interaction.py                # Form filling and submission
├── 6_interactive_page_playwright.py     # Interactive pages with Playwright
├── 7_infinite_scroll_playwright.py      # Infinite scroll with Playwright
├── 8_form_playwright_1.py               # Form handling (Playwright v1)
├── 8_form_playwright_2.py               # Form handling (Playwright v2)
├── chromedriver.exe                     # ChromeDriver executable
└── README.md                            # This file
```

## ✅ Prerequisites

Before running these scripts, ensure you have:

- Python 3.11 or higher installed
- Google Chrome or Brave browser installed
- Basic understanding of HTML and CSS selectors
- Command line/terminal knowledge

## 📦 Installation

### 1. Clone or Download the Project

```bash
git clone <your-repository-url>
cd web-scraping-project
```

### 2. Install Required Python Packages

**For Selenium scripts:**
```bash
pip install selenium beautifulsoup4
```

**For Playwright scripts:**
```bash
pip install playwright
python -m playwright install
```

**Install all at once:**
```bash
pip install selenium playwright beautifulsoup4
```

### 3. Download ChromeDriver

- Visit [ChromeDriver Downloads](https://chromedriver.chromium.org/downloads)
- Download the version matching your Chrome browser
- Place `chromedriver.exe` in the project folder
- **Or** add it to your system PATH

### 4. Verify Installation

```bash
python --version          # Should show Python 3.11+
pip list                  # Should show selenium, playwright, beautifulsoup4
```

## 📝 Scripts Description

### Selenium Scripts

#### `1_basic_scraping.py`
- **Purpose:** Introduction to Selenium basics
- **What it does:** Opens a browser, navigates to a page, extracts basic content
- **Techniques:** WebDriver setup, element location, text extraction

#### `2_dynamic_content.py`
- **Purpose:** Handle dynamically loaded content
- **What it does:** Waits for content to load before extraction
- **Techniques:** Implicit/explicit waits, dynamic element handling

#### `3_infinite_scroll_selenium.py`
- **Purpose:** Scrape content from infinite scroll pages
- **What it does:** Automatically scrolls and collects quotes
- **Techniques:** JavaScript execution, scroll detection, duplicate prevention

#### `4_infinite_scroll_comparison.py`
- **Purpose:** Compare different infinite scroll implementations
- **What it does:** Shows two approaches to infinite scrolling
- **Techniques:** Standard Selenium vs Undetected ChromeDriver

#### `5_form_interaction.py`
- **Purpose:** Automate form filling and login
- **What it does:** Logs into a website and extracts protected content
- **Techniques:** Form field interaction, button clicking, authentication

### Playwright Scripts

#### `6_interactive_page_playwright.py`
- **Purpose:** Introduction to Playwright
- **What it does:** Basic page interactions with modern syntax
- **Techniques:** Playwright setup, modern selectors, async operations

#### `7_infinite_scroll_playwright.py`
- **Purpose:** Infinite scroll with Playwright
- **What it does:** Handles infinite scroll using Playwright's API
- **Techniques:** Playwright scroll handling, wait strategies

#### `8_form_playwright_1.py` & `8_form_playwright_2.py`
- **Purpose:** Form automation with Playwright
- **What it does:** Two different approaches to form handling
- **Techniques:** Modern form interaction, validation, error handling

## 🚀 Usage Examples

### Running a Basic Selenium Script

```python
# Example: Running 3_infinite_scroll_selenium.py

from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
import time

# Setup
chrome_driver_path = "chromedriver.exe"
service = Service(executable_path=chrome_driver_path)
driver = webdriver.Chrome(service=service)

# Navigate and scrape
url = "http://quotes.toscrape.com/scroll"
driver.get(url)

# Scroll and collect quotes
quotes_set = set()
for i in range(3):
    driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
    time.sleep(2)
    quotes = driver.find_elements(By.CLASS_NAME, "quote")
    for quote in quotes:
        text = quote.find_element(By.CLASS_NAME, "text").text
        quotes_set.add(text)

driver.quit()
print(f"Collected {len(quotes_set)} unique quotes")
```

### Running a Playwright Script

```python
# Example: Basic Playwright usage

from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()
    page.goto("http://quotes.toscrape.com")
    
    # Extract quotes
    quotes = page.query_selector_all(".quote .text")
    for quote in quotes:
        print(quote.inner_text())
    
    browser.close()
```

## 🎓 Key Concepts Learned

### 1. **Web Scraping Fundamentals**
   - DOM navigation
   - CSS selectors and XPath
   - HTML structure understanding

### 2. **Selenium Techniques**
   - WebDriver configuration
   - Element location strategies (ID, Class, CSS, XPath)
   - Waiting strategies (implicit, explicit)
   - JavaScript execution
   - Browser options and customization

### 3. **Playwright Features**
   - Modern async/sync API
   - Auto-waiting mechanisms
   - Network interception
   - Multiple browser support

### 4. **Dynamic Content Handling**
   - Infinite scroll detection
   - AJAX content loading
   - Dynamic element waiting

### 5. **Form Automation**
   - Input field interaction
   - Button clicking
   - Form submission
   - Authentication handling

### 6. **Best Practices**
   - Respectful scraping (delays, rate limiting)
   - Error handling
   - Resource cleanup (driver.quit())
   - Duplicate prevention

## 🔧 Troubleshooting

### Common Issues and Solutions

#### Issue: "chromedriver.exe not found"
```bash
# Solution 1: Specify full path
chrome_driver_path = r"C:\path\to\chromedriver.exe"

# Solution 2: Add to PATH or place in project folder
```

#### Issue: "Module not found"
```bash
# Install missing packages
pip install selenium playwright beautifulsoup4
```

#### Issue: "Browser version mismatch"
```bash
# Download ChromeDriver matching your Chrome version
# Check Chrome version: chrome://version
# Download from: https://chromedriver.chromium.org/downloads
```

#### Issue: Kernel taking too long to connect (Jupyter)
```bash
# Restart kernel
# Close other notebooks
# Check Task Manager for stuck Python/ChromeDriver processes
```

#### Issue: "playwright command not found"
```bash
# Use Python module syntax instead
python -m playwright install
```

#### Issue: Elements not found
```python
# Add wait time
import time
time.sleep(2)

# Or use explicit waits
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

element = WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.ID, "element_id"))
)
```

## 📚 Resources

### Official Documentation
- [Selenium Documentation](https://selenium-python.readthedocs.io/)
- [Playwright Python Documentation](https://playwright.dev/python/)
- [BeautifulSoup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

### Practice Sites
- [Quotes to Scrape](http://quotes.toscrape.com/) - Main practice site
- [Books to Scrape](http://books.toscrape.com/) - E-commerce scraping
- [Scrape This Site](https://www.scrapethissite.com/) - Various challenges

### Learning Resources
- [Platzi Web Scraping Course](https://platzi.com/) - Course materials
- [Real Python - Web Scraping](https://realpython.com/tutorials/web-scraping/)
- [Automate the Boring Stuff](https://automatetheboringstuff.com/)

### Tools
- [ChromeDriver Downloads](https://chromedriver.chromium.org/downloads)
- [CSS Selector Tester](https://try.jsoup.org/) - Test selectors
- [XPath Tester](http://xpather.com/) - Test XPath expressions

## ⚖️ Legal and Ethical Considerations

- Always check a website's `robots.txt` file
- Respect rate limiting and server resources
- Only scrape publicly available data
- Follow the website's Terms of Service
- Use appropriate delays between requests
- Don't overwhelm servers with requests

## 🤝 Contributing

This is a learning project, but suggestions and improvements are welcome!

## 📄 License

This project is for educational purposes. Practice responsibly!

## 👤 Author

**Tiger**
- Learning web scraping through Platzi courses
- Data Analyst at Stellantis
- [LinkedIn](https://linkedin.com/in/your-profile)

---

**Happy Scraping! 🎉**

*Remember: With great scraping power comes great responsibility. Always scrape ethically and respectfully.*
