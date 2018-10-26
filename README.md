# selenum을 이용한 웹 크롤러 만들기.
[참고 사이트](https://beomi.github.io/2017/02/27/HowToMakeWebCrawler-With-Selenium/)

## selenium이란?
* Selenium은 주로 웹앱을 테스트하는 프레임워크입니다. webdriver라는 API를 통해 운영체제에 설치된 Chrome등의 브라우저를 제어합니다.

## 실행 브라우저
* Chrome
## 개발 언어
* Python3.x

# seleum 크롤링과 텔레그램 봇 연동 샘플코드
* 크롬드라이버가 필요합니다. [다운로드 사이트](http://chromedriver.chromium.org/downloads)
```
from selenium import webdriver 
import telegram

#텔레그렘 봇의 API 키를 가져옵니다. 
bot = telegram.Bot(token = '텔레그램 봇의 키 입력')
chat_id = '알람 받을 채팅방의 채팅id 입력'

driver = webdriver.Chrome('크롬드라이버의 경로입력')
driver.implicitly_wait(3)
driver.get('파싱하고 싶은 웹 주소 입력')

#아이디와 비번을 입력해줍니다. (로그인이 필요한 경우) 
driver.find_element_by_name('아이디 엘레먼트 네임을 입력').send_keys('아이디 입력') 
driver.find_element_by_name('비밀번호 엘레먼트 네임을 입력').send_keys('비번 입력') 
#로그인버튼 클릭 
driver.find_element_by_xpath('로그인버튼의 xpath입력').click()

ex) 제목파싱하여 메시지 알람 
# xpath 이용하여 제목 파싱 
latest = driver.find_element_by_xpath('//*[@id="listView"]/div[1]/div[1]/a/h3').text.split('[')
#텔레그램봇에게 메시지를 보냅니다.
bot.sendMessage(chat_id=chat_id, text='테스트 중') 
bot.sendMessage(chat_id=chat_id, text='주제 : '+latest[0])

```
