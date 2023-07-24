---
weight: 800
title: "Selenium"
---

Docs:

- [Selenium with Python — Selenium Python Bindings 2 documentation](https://selenium-python.readthedocs.io/index.html)
- [Selenium Client Driver — Selenium 4.10 documentation](https://www.selenium.dev/selenium/docs/api/py/index.html)

## Basics

Starting up:

```python
from selenium import webdriver
driver = webdriver.Chrome (executable_path="C:\\chromedriver.exe")
```


Get text: `element.get_attributes("innerHTML")` \(`.text` sometimes does not work\) \([ref](https://stackoverflow.com/a/8575709/10668706)\)

Go back: `driver.back()`


## Selectors

### XPATH

`.\\` for relative \(chained after other elements\), `\\` for absolute \(starting from `body`\)


## Scroll to and click

[python - Scrolling to element using webdriver? - Stack Overflow](https://stackoverflow.com/a/41744403/10668706)

```python
from selenium.webdriver.common.action_chains import ActionChains

link = driver.find_element_by_id("my-id")
ActionChains(driver).move_to_element(link).click(link).perform()
```
