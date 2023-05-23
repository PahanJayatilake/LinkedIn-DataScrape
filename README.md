# LinkedIn-DataScrape

#Import Packages
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from bs4 import BeautifulSoup

from selenium.webdriver.chrome.options import Options
chrome_options = Options()
chrome_options.add_experimental_option("detach", True)

import time
#import pandas as pd
import json

class Browser:
        browser, service = None, None

        def __init__(self, driver: str):
            self.service = Service(driver)
            self.browser = webdriver.Chrome(service=self.service)

        def open_page(self, url: str):
            self.browser.get(url)

        def close_browser(self):
            self.browser.close()


        def add_input(self, by: By, value: str, text: str):
            field = self.browser.find_element(by=by, value=value)
            field.send_keys(text)
            time.sleep(1)

        def click_button(self, by: By, value: str):
            button = self.browser.find_element(by=by, value=value)
            button.click()
            time.sleep(1)


        def login_linkedin(self, username: str, password: str):
            self.add_input(by=By.ID, value= 'session_key', text=username)
            self.add_input(by=By.ID, value= 'session_password', text=password)
            self.click_button(by=By.XPATH, value="//button[normalize-space()='Sign in']")
            time.sleep(3)


        def type_linkedin_searchbar(self, title: str):
            self.add_input(by=By.XPATH, value="//input[@placeholder='Search']", text=title)
            time.sleep(5)


if __name__ == '__main__':
    browser = Browser('C:/Users:/Users/pahan/chromedriver.exe')

    browser.open_page('https://www.linkedin.com')
    time.sleep(3)

    browser.login_linkedin(username='chensawman598@gmail.com',password='DenjixPochita9876')
    time.sleep(10)

    browser.type_linkedin_searchbar(title='NanoEngineering')
    time.sleep(5)



    browser.close_browser()
