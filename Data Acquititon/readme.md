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
