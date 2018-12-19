# SSAFY-DAY1

## 첫번째시간

### 자기소개

- 전공
- 지원동기
- 포부

###  여러가지언어

- python
- Web-HTML/CSS
- Framework-flask/Django
- Git, Amazon Web Services(개발자라면 알아야되는 언어)

### 포트폴리오 관리 방법

- Typora

### 구글 딥마인드의 최신병기 알파폴드(AlphaFold)

### computation이란

- 컴퓨터에 의해 실행되는 지시사항의 모음
- 사용자의 입력에 반응하도록 명령하는 것

### 챗봇 사이트

- https://gj.py.hphk.io/vots



### 파이썬 랜덤함수

```python
import random #랜덤 함수 정의
menu = ["삼겹살","김밥","닭갈비","돈까스","소고기"]
# 메뉴 리스트
pick = random.choice(menu) # 외부에서 가져오는 공구툴/한개만 가져옴
print(pick)#출력
```

- 두번째 랜덤함수(pick과 phonebook 데이터값 불러오기)

```python
import random #랜덤 함수 정의
menu = ["삼겹살","김밥","닭갈비","돈까스","소고기"]
# 메뉴 리스트
pick = random.choice(menu) # 외부에서 가져오는 공구툴/한개만 가져오기
print(pick)

phonebook = {'삼겹살':'010-8584-7295',
             '김밥':'010-8584-7',
             '닭갈비':'010-8584-75',
             '돈까스':'010-8584-',
             '소고기':'010-8584-295',
            }
print(phonebook[pick])
```



### 파이썬 반복문 while

- true  일때까지 반복적으로 실행됨

```python
n=0
while n<3:
  print("출력")
  n=n+1
```

- 2번째 소스

```python
dust=[59,24,102,45,64]
n=0
while n<3:
  print(dust[n])
  n=n+1

```

### 파이썬 반복문 for

- for i in List: 어떤 범위내의 값을 반복하는 작업

```python
dust = [59,24,102]
for i in dust:
  print(i)
```

- 2번째 소스

```python
dust = ["안녕하세요","안녕하세요","안녕하세요","안녕하세요","안녕하세요","안녕하세요","안녕하세요","안녕하세요","안녕하세요","안녕하세요"]
for i in dust:
```



### 파이썬 조건문 if

```python
import requests
from bs4 import BeautifulSoup
url = 'http://openapi.airkorea.or.kr/openapi/services/rest/ArpltnInforInqireSvc/getCtprvnRltmMesureDnsty?serviceKey=' + key + '&numOfRows=10&pageSize=10&pageNo=1&startPage=1&sidoName=%EA%B4%91%EC%A3%BC&ver=1.3'
request = requests.get(url).text
soup = BeautifulSoup(request,'xml')
dong = soup('item')[7]
location = dong.stationName.text
time = dong.dataTime.text
dust = int(dong.pm10Value.text)

print("{0} 기준 {1}의 미세먼지 농도는 {2}입니다.".format(time,location,dust))

if dust<30: #파이썬에서는 부등호 두개를 사용할수있다.
  print("좋음")
elif dust<80:
  print("보통")
elif dust<150:
  print("나쁨")
else:
  print("매우나쁨")
```

- 실행결과

2018-12-17 14:00 기준 오선동의 미세먼지 농도는 74입니다.

보통

- 강사님 코드

```python
#강사님 코드
import requests
from bs4 import BeautifulSoup
url = 'http://openapi.airkorea.or.kr/openapi/services/rest/ArpltnInforInqireSvc/getCtprvnRltmMesureDnsty?serviceKey=' + key + '&numOfRows=10&pageSize=10&pageNo=1&startPage=1&sidoName=%EA%B4%91%EC%A3%BC&ver=1.3'
request = requests.get(url).text
soup = BeautifulSoup(request,'xml')
dong = soup('item')[7]
location = dong.stationName.text
time = dong.dataTime.text
dust = int(dong.pm10Value.text)

print("{0} 기준 {1}의 미세먼지 농도는 {2}입니다.".format(time,location,dust))
if(dust > 150):
  print("매우나쁨입니다. 마스크 착용하세요")
elif (80 < dust <=150):
  print("나쁨입니다.")
elif (30 < dust and dust <= 150):
  #파이썬에서는 아래와 같이 부등호를 양 옆에 쓸 수 있다.
  print("보통입니다.")
else:
  print("공기가 좋아요.")  
```

### &_returnType=jason

- jason 값 불러온다.



### API

- 다른 시스템 간의 커뮤니케이션 방식
- 프로그램과 프로그램간의 인터페이스 규칙
- 서비스와 서비스간의 대화방식
- 요청을 받는 측에서 일정한 방식을 명세



### 웹에서의 커뮤니케이션 방식

- 요청과 응답
- 요청은 주소 Url- 응답은 XML,HTML,JASON
- IBM- Watson Personality insights 성격인사이트 



### 여러가지함수

- abs() 절대값
- len() 길이출력
- random.choice() 랜덤 인덱스 불러옴
- random.sample(리스트,개수)-배열에서 특정 수의  요소를 임의적으로 비복원추출



### 랜덤 6개 뽑기

```python
import random
#numbers에 1부터 45넣기
numbers = list(range(1,46))#그냥range는 객체 리스트를 짜야됨 그래서 list로 배열 만들어줌
a=random.sample(numbers,6) #choice 는 1개의 객체를 랜덤으로 뽑아줌
print(a)
```



### url간단하게 쓰는 방법

```python

import requests

url = 'https://finance.naver.com/sise/'

r = requests.get(url)#정상적인 작동을 보여줌
print(r)
```

```python
import requests

url = 'https://finance.naver.com/sise/'

r = requests.get(url).text# 여러가지 실행결과를 보여줌
print(r)

```

### 파이썬 내부검색을 보기 편하게 쓰는법

```python
import requests
from bs4 import BeautifulSoup #파이썬 내부 검색을 보기 편하게 쓰는 모듈
url = 'https://finance.naver.com/sise/'

r = requests.get(url).text
soup = BeautifulSoup(r,'html.parser')#옵션줌
print(soup)
```

### 크롤링한 데이터 내부 코드 찾는법

```python
import requests
from bs4 import BeautifulSoup #모듈
url = 'https://finance.naver.com/sise/'

r = requests.get(url).text
soup = BeautifulSoup(r,'html.parser')#옵션줌 ,알아보기힘든걸 알아보기쉽게 보여줌 ,필요한값을 가져온다.
select=soup.select_one("#KOSPI_now")#특정값을 전달받음
print(select)#여기에 (select.text) 를 넣으면 출력 2,071.09

```

