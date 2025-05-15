# Airbnb-Test-with-Pytest-Playwright
Here’s the complete **README.md** for your project:

---

# Airbnb Automation Test Suite

**Automated end-to-end tests** for the Airbnb web application using Playwright and pytest. This suite covers searching for stays, validating results, selecting and reserving listings, and verifying reservation workflows.

---

## Table of Contents

1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Configuration](#configuration)
5. [Project Structure](#project-structure)
6. [Running Tests](#running-tests)
7. [Generating Reports](#generating-reports)
8. [Page Object Model](#page-object-model)
9. [Validation Utility](#validation-utility)
10. [Logging & Screenshots](#logging--screenshots)
11. [Contributing](#contributing)
12. [License](#license)

---

## Features

* **Search Workflow**: Enter destination, dates, and guest counts.
* **Search Results**: Handle popups, filter cheapest or highest-rated listings.
* **Listing Validation**: Verify listing details before reservation.
* **Reservation Flow**: Complete reservation steps and confirm success.
* **Headed & Headless**: Run tests in both modes via CLI flag.
* **Allure Reporting**: Capture logs, screenshots, and generate rich reports.

---

## Prerequisites

* **Python** 3.8+
* **Node.js** (for Playwright browser binaries)
* **Git** client

---

## Installation

1. **Clone the repository**

   ```bash
   git clone <repository_url>
   cd <repository_folder>
   ```
2. **Set up virtual environment**

   ```bash
   python -m venv .venv
   source .venv/bin/activate   # macOS/Linux
   .venv\Scripts\activate      # Windows
   ```
3. **Install Python dependencies**

   ```bash
   pip install -r requirements.txt
   ```
4. **Install Playwright browsers**

   ```bash
   playwright install
   ```

---

## Configuration

* **helper/config.py**:

  * `URL` – base URL of Airbnb.
  * `VALID_CREDENTIALS` – default search parameters (destination, dates, guests).
* **pytest.ini**: Configure pytest options, e.g. add `--headed` for headed mode.

---

## Project Structure

```
├── helper/                
│   ├── config.py          # Base URL & test data generator
│   ├── utils.py           # Logging, screenshot, random date utils
│   └── validation.py      # AppValidation helper class
├── page_objects/          
│   ├── base_page.py       # BasePage with common actions
│   ├── home_page.py       # Home page interactions
│   ├── search_result_page.py # Handling search results
│   ├── listing_page.py    # Listing page checks
│   └── reserve_page.py    # Reservation workflow
├── tests/                 
│   └── test_home.py       # End-to-end test scenario
├── conftest.py            # Pytest fixtures and setup
├── pytest.ini             # Pytest configuration
├── requirements.txt       # Python package dependencies
└── README.md              # This documentation
```

---

## Running Tests

* **Default (headless)**:

  ```bash
  pytest
  ```
* **Headed mode**:

  ```bash
  pytest --headed
  ```
* **With Allure**:

  ```bash
  pytest --alluredir=allure-results -v -s
  ```

---

## Generating Reports

1. Install [Allure CLI](https://docs.qameta.io/allure/).
2. Serve results:

   ```bash
   allure serve allure-results
   ```

---

## Page Object Model

* **BasePage** (`page_objects/base_page.py`):

  * `safe_execute` for robust actions.
  * Common helpers: `click_element`, `fill_element`, `navigate_to`.
* **HomePage** (`home_page.py`):

  * Search form manipulation and submission.
* **SearchResultPage** (`search_result_page.py`):

  * Filter and open listings based on price or rating.
* **ListingPage** (`listing_page.py`):

  * Validate listing details and proceed to reservation.
* **ReservePage** (`reserve_page.py`):

  * Fill reservation form and verify confirmation.

---

## Validation Utility

* **AppValidation** (`helper/validation.py`):
  Inherits from `BasePage` to orchestrate end-to-end validations across all page objects.

---

## Logging & Screenshots

* Use `log_message` (`helper/utils.py`) to record INFO/DEBUG/WARNING/ERROR levels.
* On failures, `take_screenshot` captures the browser state and attaches to Allure.

---



