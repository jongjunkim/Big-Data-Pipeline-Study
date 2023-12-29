# Data Acquisition

Data Acquisition is the step where you obtain data through one or more of the following methods:

1. Obtain data either for free or by purchasing it.
2. Use specialist web scraper technology or simply copy-paste.
3. Fetch data from internal or external sources.

## Crawling

Crawling involves exploring and collecting information from the web.

- Web scraping to navigate and gather information.
- The `urlopen` function can be used to retrieve data from the website.

## Scraping
- 특정웹사이트에서 웹페이지에서 필요한 데이터를 자동 추출하는 것
-	Scraping data does not necessarily involve the web
-	Data scraping could refer to extracting information from a local machine, a database, or even if it is from the internet
-	`BeautifulSoup` is a Python lib, for pulling data out of HTML & XML files
  
## Selenium(Web Browser Scraping)
-	자바스트립트가 동적으로 만든 데이터 크롤링
-	사이트의 다양한 HTML 요소에 클릭, 키보드 입력 등 이벤트 부여가능
-	평소 반복적으로 하고 있느 Web site 업무 자동화
-	자동을 로그인, 메일보내기 자동화, 블로그 이웃새글 자동좋아요
-	링크드인 자동 어플라이

## 실습

- Ubuntu 환경에서 python virtual environment 설치
- Python3 –m pip install –user –U virtualenv
- Python3 –m virtualenv venv
- Source venv/bin/activate
- (이렇게하면 python의 라이브러들을 isolated 환경에서 구현가능 python1, 2, 3 이것들을 따로 실행가능)

### Example:

#### 기상청RSS Urllib 이용해서 Crawling 하기
```python
#1/usr/bin/env python3  <- 이렇게 주석을 달아주는 이유는 밑에 import들이 python3로 실행 하기 위해서 필요함 (`Shebang` 샤벵이라고 불림)
import sys
import urllib.request as req
import urllib.parse as parse

if len(sys.argv) <= 1:
    print("usage: download-forecast-argv <region number>")
    sys.exit()

regionNumber = sys.argv[1]

api_addr = "http://www.kma.go.kr/weather/forecast/mid-term-rss3.jsp"
values = {
        'stnId' : regionNumber
}

params = parse.urlencode(values)
url = api_addr + "?" + params
print{"url =", url}
data = req.urlopen(url).read()
text = data.decode("utf-8")
print(text)
```
#### 기상청RSS Beautilful soup 이용해서 crawling
```python
#1/usr/bin/env python3

import requests
from bs4 import BeautifulSoup

def main():
    url = "http://www.kma.go.kr./weather/forecast/mid-term-rss3.jsp"
    res = requests.get(url)

    soup = BeautifulSoup(res.text)
    locations = soup.find_all("location")

    for location in locations:
        city = location.find("city").text
        date = location.find("data").find("tmef").text
        weather = location.find("data").find("wf").text

        print(f"[ {date} , {city} : {weather}")

if __name__ == "__main__":
    main()
```
#### 네이버 finance에서 실시간 달러환율 정보 가져오기
```python
from bs4 import BeautifulSoup
import urllib.request as req
import datetime

url = "https://finance.naver.com/marketindex/"
now = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

res = req.urlopen(url).read()

soup = BeautifulSoup(res, "html.parser")
currency = soup.select_one("#exchangeList > li.on > a.head.usd > div > span.value")
print(now, currency.string)
```
#### Selenium 이용해서 자동으로 사이트 열게 하기
```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome('/home/rkdlem196/2023_BIGDATA/driver/chromedriver')
driver.implicitly_wait(2)
driver.get('https://www.daum.net/')
```

# Recursive Web Crawling and Task Automation

1. **Analyze HTML File:**
   - Parse the HTML content to extract relevant information.

2. **Extract Links:**
   - Utilize tools like BeautifulSoup to identify and extract hyperlinks from the HTML.

3. **Download Links (If File):**
   - Check if the extracted link points to a file.
   - If yes, download the file using appropriate methods.

4. **Recursive HTML Crawling:**
   - If the file is an HTML document, repeat the process by going back to step 1.

# Web API

- **Definition:**
  - Web API acts as an intermediary between a client (HTTP REQUEST) and a server (HTTP RESPONSE).
  
- **Analogy:**
  - Think of it as a waiter (API) taking orders from a customer (Client), communicating with the kitchen (Server), and delivering the requested items back to the customer.

- **Features:**
  - *Side Effect:* Web APIs can induce changes or have side effects.

- **Dynamic Nature:**
  - Web API addresses may change over time.

# Scheduler

- **Introduction:**
  - Scheduling tasks is crucial for automation and recurring processes.

- **Cron Daemon:**
  - Linux has a handy scheduling daemon called cron.
  - It's a long-running process that executes commands at specific times.

- **Usage:**
  - Schedule activities, either as one-time events or as recurring tasks.

- **Cron Syntax:**
  - `*(분 0-59) *(시간 0-23) *일(1-31) *월(1-12) *요일(0-7)`

# Crontab Cheatsheet

- **Load from File:**
  - `File`: Load the crontab data from the specified file.

- **User-Specific View:**
  - `-u user`: Specifies the user whose crontab is to be viewed.

- **Display Current Crontab:**
  - `-l`: Display the current crontab.

- **Remove Crontab:**
  - `-r`: Remove the current crontab.

- **Edit Crontab:**
  - `-e`: Edit the current crontab, using the editor specified in the environment variable VISUAL or EDITOR.

# Proxy Server Motivation

When sending a large number of requests to a specific target service for web scraping, or making prolonged requests, the target service might detect and limit access. To overcome this, a Proxy Server is employed.

## Proxy Server Features:

- **Security:**
  - Other anonymous users can't easily determine the location or IP address of the server.

- **Cache:**
  - Previous requests are stored in the Proxy Server's cache, allowing for faster responses when the same data is requested again.

- **Rotate:**
  - Like the first security feature, rotating IP addresses adds an extra layer of anonymity, making it difficult to track where the client is connecting from.

## Proxy Server Types:

- **Forwarded Proxy:**
  - When the client sends a request to the server, it doesn't go directly; instead, it passes through the Proxy Server.

- **Reverse Proxy:**
  - In contrast to a Forwarded Proxy, a Reverse Proxy sits on the server side and handles requests from clients. It forwards those requests to the actual server, acting as an intermediary.

## Selenium Automation Example: 링크드인 접속해서 자동으로 로그인후 python을 검색했을때 나오는 공고 첫번째 apply 자동화

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome('/home/rkdlem196/2023_BIGDATA/driver/chromedriver-linux64/chromedriver')
driver.implicitly_wait(2)
#driver.get('https://www.daum.net/')

JOB_URL = "https://www.linkedin.com/jobs/search/?currentJobId=3291207294&geoId=103588929&keywords=PYTHON&location=%EB%8C%80%ED%95%9C%EB%AF%BC%EA%B5%AD%20%EC%84%9C%EC%9A%B8&refresh=true" 
driver.get(JOB_URL)

login = driver.find_element(By.CSS_SELECTOR, ".btn-secondary-emphasis")
login.click()

username = driver.find_element(By.ID, "username")
username.send_keys("~~~~~~~")

password = driver.find_element(By.ID, "password")
password.send_keys("~~~~~~~~!")

login_button = driver.find_element(By.CSS_SELECTOR, ".from__button--floating")
login_button.click()

driver.implicitly_wait(5)
apply_button = driver.find_element(By.CSS_SELECTOR, ".jobs-apply-button--top-card button")
apply_button.click()
```

## Crontab이용해서 scheduler 실행하기
1. crontab -e
2. * * * * * python3 /home/rkdlem196/2023_BIGDATA/data_acquisition/4_market.py 
- /home/rkdlem196/BIGDATA/data_acquisition/market.log
4. crontab –l 하면 scheduling한게 보임



