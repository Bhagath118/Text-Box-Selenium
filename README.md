# Text-Box-Selenium

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.common.exceptions import StaleElementReferenceException
from selenium.webdriver.support.ui import Select, WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
wait = WebDriverWait(
    driver,
    10,
    ignored_exceptions=(StaleElementReferenceException,)
)
current_step = "opening the registration page"

try:
    # 1. Open website
    driver.get("https://vinothqaacademy.com/demo-site/")

    # 2. Maximize browser
    driver.maximize_window()

    def fill_field(locator, value):
        for attempt in range(3):
            element = wait.until(EC.visibility_of_element_located(locator))
            try:
                element.clear()
                element.send_keys(value)
                return
            except StaleElementReferenceException:
                if attempt == 2:
                    raise

    def select_choice(locator):
        for attempt in range(3):
            element = wait.until(EC.element_to_be_clickable(locator))
            try:
                if not element.is_selected():
                    element.click()
                return
            except StaleElementReferenceException:
                if attempt == 2:
                    raise

    # 3. First Name
    current_step = "filling First Name"
    fill_field((By.ID, "vfb-5"), "Bhagath")

    # 4. Last Name
    current_step = "filling Last Name"
    fill_field((By.ID, "vfb-7"), "Krishna")

    # 5. Gender - Male
    current_step = "selecting Male"
    select_choice((By.ID, "vfb-31-1"))

    # 6. Course - Selenium WebDriver
    current_step = "selecting Selenium WebDriver"
    select_choice((By.ID, "vfb-20-0"))

    # 7. Street Address
    current_step = "filling Street Address"
    fill_field((By.ID, "vfb-13-address"), "Chennai")

    # 8. Apt / Suite
    current_step = "filling Apt / Suite"
    fill_field((By.ID, "vfb-13-address-2"), "A1")

    # 9. City
    current_step = "filling City"
    fill_field((By.ID, "vfb-13-city"), "Chennai")

    # 10. State
    current_step = "filling State"
    fill_field((By.ID, "vfb-13-state"), "Tamil Nadu")

    # 11. Postal Code
    current_step = "filling Postal Code"
    fill_field((By.ID, "vfb-13-zip"), "600001")

    # 12. Country
    current_step = "selecting Country"
    for attempt in range(3):
        country = wait.until(
            EC.element_to_be_clickable((By.ID, "vfb-13-country"))
        )
        try:
            Select(country).select_by_visible_text("India")
            break
        except StaleElementReferenceException:
            if attempt == 2:
                raise

    # 13. Email
    current_step = "filling Email"
    fill_field((By.ID, "vfb-14"), "bhagath@example.com")

    # 14. Date
    current_step = "filling Date of Demo"
    fill_field((By.ID, "vfb-18"), "10/06/26")

    # 15. Mobile Number
    current_step = "filling Mobile Number"
    fill_field((By.ID, "vfb-19"), "9876543210")

    # 16. Query / Text Area
    current_step = "filling Query"
    fill_field(
        (By.ID, "vfb-23"),
        "I am learning Selenium automation testing."
    )

except Exception as error:
    print(
        f"\nAutomation failed while {current_step}: "
        f"{type(error).__name__}: {error}"
    )
    input("Browser is paused. Press ENTER to close it...")
    raise
else:
    input("Automation finished. Press ENTER to close the browser...")
finally:
    driver.quit()


<img width="1907" height="941" alt="Screenshot 2026-10-06 115735" src="https://github.com/user-attachments/assets/e12d5e05-01ac-421b-905d-f359c6d7c31d" />

