# SSAFY-DAY3

## 첫번째시간

### 앞으로 자기할말 등록사이트

- zzu.li/pygj

### 

### C9에 Simple Python Version Management: pyenv 다운로드방법

쉬운 파이썬 설치



pyenv  >>https://github.com/pyenv/pyenv>> Simple Python Version Management: pyenv 다운로드(파이썬 환경 관리 프로그램) >>목차 >> Installation >> Basic GitHub Checkout따라하기



터미널에 차례대로 복사(python2버전과 3버전을 한컴퓨터에 다루기위한 환경설정)

``` 
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
```

```
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash
```

```
exec "$SHELL"
```

```
pyenv -v
```

출력결과 pyenv 1.2.8-5-gec9fb549

### 파이썬 2버전 확인방법(3버전과 다른 언어 - 문법이 달라서)

```
python -V
```

출력결과 Python 2.7.6 이런식으로 버전뜸 ※대문자 체크 잘해줘야됨!!

### 파이썬 3버전 확인방법

```
python3 -V
```

출력결과 Python 3.4.3 ※대문자 체크 잘해줘야됨!! 소문자로들어가게되면  Shell로 들어가게됨

### 오류 탈출방법

```
exit()
```

### 파이썬 설치할수있는 버전 확인

```
pyenv install -list
```

### 파이썬 3.6.7 설치(안정화 되어있는 가벼운버전)

```
pyenv install 3.6.7
```

### 파이썬 3.6.7 사용할수있게 글로벌 설정해주는 법

```
pyenv global 3.6.7
pyenv rehash
```

### 파이썬 버전 (pyenv가 설정해준것을 확인)

```
pyenv versions
```

출력  system

* 3.6.7 (set by /home/ubuntu/.pyenv/version)

### 폴더 확인

```
ls
```

### 폴더생성

```
mkdir email
```

### 폴더들어가기

```
cd email
```

### 파일생성

```
touch send_email.py
```

### 안에 코드 실행

```
python send_email.py
```



#### 네이버 메일에서 이메일보낼때 환경설정하는 방법

##### 네이버 메일>>환경설정 >>POP3/SMTP설정>>POP3/SMTP사용 설정



### 이메일보내기

```
import smtplib
from email.message import EmailMessage
import getpass

password= getpass.getpass('비밀번호 뭐니') #비밀번호 물어보기 커맨드창

msg = EmailMessage()#EmailMessage변수저장
msg['Subject']="제목은 제목입니다!!!" #설정해줌 딕셔너리접근
msg['From'] = "pok_kjy@naver.com"#누가 보내는지
msg['To']="rn021548@naver.com"#누구에게 보낼지
msg.set_content('내용은 내용입니다!!')#내용작성

smtp_url = 'smtp.naver.com'#SMTP 서버명(건물)
smtp_port = 465  #PORT 접속(문) SMTP포트※POP포트 아니다!!

s=smtplib.SMTP_SSL(smtp_url,smtp_port)#보안연결을위해 하는것(어디건물,어디문)
#비밀번호 방식이 SSL

s.login('pok_kjy',password) #아이디와 패스워드
s.send_message(msg)#메세지 보내게하는 명령어

```

터미널실행

```
python send_email.py
```

##### 출력결과 비밀번호 뭐니가 뜨는데 이때 비밀번호를 치면된다. 치는게안보여도 쳐지는것!!



```
컨트롤+c #터미널 초기화
알트+t #터미널 생성
F6 #터미널 내리기
컨트롤+s #저장


터미널생성할경우에 다시 파일에 들어가야됨
cd email
```



##### 갑자기 수업을 놓칠때 https://다른사람주소 치면됨!!





#### 리스트를 불러오고 확인

```
import csv

f= open('pygj - email.csv','r',encoding='utf-8')#r은 email 을 읽음 encoding 파일을 열어줌
read_csv =csv.reader(f) #csv를 열어주는 함수
for line in read_csv:
    print(line[0]+'/'+line[1])#0~1라인사이에 /를 넣고 출력
    
    
f.close()
```



### 리스트를 불러와 전체 메일보내기

```python
import csv
import smtplib
from email.message import EmailMessage

import getpass

     
smtp_url = 'smtp.naver.com'#SMTP 서버명(건물)
smtp_port = 465  #PORT 접속(문)
s=smtplib.SMTP_SSL(smtp_url,smtp_port)#보안연결을위해 하는것(어디건물,어디문)
f= open('pygj - email.csv','r',encoding='utf-8')#r은 email 을 읽음 encoding 파일을 열어줌
read_csv =csv.reader(f) #csv를 열어주는 함수
    
password= getpass.getpass('비밀번호 뭐니 : ') #비밀번호 물어보기 커맨드창

s.login("pok_kjy@naver.com",password) #아이디와 패스워드
for line in read_csv:
    print(line)
    print(line[0]+'/'+line[1])#0~1라인사이에 /를 넣고 출력
    email_list = line[1]
    msg = EmailMessage()#EmailMessage변수저장
    msg['Subject']="제목은 제목입니다!!!" #설정해줌 딕셔너리접근
    msg['From'] = "pok_kjy@naver.com"#누가 보내는지
    msg['To']=email_list#누구에게 보낼지
    msg.set_content('내용은 내용입니다!!')#내용작성
    #msg.add_alternative('''<h1>안녕</h1><p>난은솔이야</p>''',subtype="html") 
    #이 코드넣으면 주제 부제 넣을수있음

 
    s.send_message(msg)
    
f.close()
 #email list 변수저장
    
```



#### 폴더 나가기

``` 
cd ..
```



### 플라스크 맛보기

```
http://flask.pocoo.org/
```

##### 여기에 들어간 후 첫번째 코드

```python
from flask import Flask
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "안녕하세요" #안녕하세요를 반환
```

##### 이코드 넣자!

### 플라스크 설치 코드

```
pip install Flask
pip list
```

##### 터미널에 넣자

#### 플라스크 app.py 실행

```
FLASK_APP=app.py flask run
```

#### 플라스크

```
FLASK_APP=app.py flask run --host=$IP --port=$PORT #파일불러온후 FLASK 실행 $IP와PORT로 준다.
```

##### 출력

```
* Serving Flask app "app.py"
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
10.240.1.191 - - [19/Dec/2018 04:39:00] "GET / HTTP/1.1" 200 -
```

### 플라스크에서 라우트 설정(경로설정)

```python
from flask import Flask
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
```

##### 이렇게 하게되면 일반경로로 들어가면 안녕하세요만 뜨지만 그주소 맨뒤에 /html_tag 을 붙이면

##### 두번째 경로가 보임



### CHROME설정법

제어판 > 시스템 및 보안  >관리도구 > 서비스 > Cryptographic Services >로그온 > 로컬 시스템 계정

### 플라스크를 사용하여 html파일 웹에 보내기

```python
from flask import Flask, render_template
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
```



#### 변수로 데이터 받아서 html로 전달하기

```python
from flask import Flask, render_template
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소
```

#### welcome.html 안에 코드

```html
<h1>{{people}}님 안녕하세요!!!</h1>
```

#### html의 기본규칙

html 형식

<태그명 속성1="속성1" 속성2="속성2"> 내용 </태그명> 

```html
<!doctype html>
<html>
    <head>
    </head>
    
    <body>
        <h3>html을 배워봅시다</h3>
        <a href="https://naver.com">naver로 가기</a>
        
    </body>
</html>
```



#### soso.html 에서 숫자 3제곱근해서 웹으로 보내기

```python
from flask import Flask, render_template
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소

@app.route("/cube/<int:num>")
def cube(num):
    return render_template("soso.html",soso=num*num*num)
```

#### 2번째 예제

```python
from flask import Flask, render_template
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소

@app.route("/cube/<int:num>")
def cube(num): #메소드에 num 을쓸수있게 함
    triple= num*num*num
    return render_template("soso.html",triple=triple,num=num)#triple과 triple은 다른 개념
    #왼쪽triple은 cube.html에서만 사용가능한 변수
    #오른쪽 triple은 파이썬에서 사용하는 변수
```

#### 3번째 밥먹기예제

```python
from flask import Flask, render_template
import random
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소

@app.route("/cube/<int:num>")
def cube(num): #메소드에 num 을쓸수있게 함
    triple= num*num*num
    return render_template("soso.html",triple=triple,num=num)#triple과 triple은 다른 개념
    #왼쪽triple은 cube.html에서만 사용가능한 변수
    #오른쪽 triple은 파이썬에서 사용하는 변수
    
@app.route('/lunch')
def lunch():
    menu=["돼지찌게","김치찌게","바보","돈까스"]
    pick = random.choice(menu)
    return render_template("httt.html",menu=pick)
```

#### 예제 4번 로또번호뽑기

```python
from flask import Flask, render_template
import random
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소

@app.route("/cube/<int:num>")
def cube(num): #메소드에 num 을쓸수있게 함
    triple= num*num*num
    return render_template("soso.html",triple=triple,num=num)#triple과 triple은 다른 개념
    #왼쪽triple은 cube.html에서만 사용가능한 변수
    #오른쪽 triple은 파이썬에서 사용하는 변수
    
@app.route('/lunch')
def lunch():
    menu=["돼지찌게","김치찌게","바보","돈까스"]
    pick = random.choice(menu)
    return render_template("httt.html",menu=pick)
    
@app.route('/rotto')#주소로들어가야 실행됨
def rotto():
    numttt = list(range(1,46))
    a=random.sample(numttt,6)
    s=sorted(a)#숫자들을 정렬해줌 오름차순정렬
    return render_template("too.html",pi=s)
    
```

#### 출력

```
[10, 19, 21, 25, 32, 39] 축하합니다 행운의벊
```



#### html 안에서 html 구조잡을때 

```
!+tap
```

#### 실행결과

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

#### html에 form+tap을 누르면

#### 실행결과

```html
<form>
        <input type="text" name=""/> #name에 naver를 적으면 주소창에 복사가됨
        <input type="submit" value="Submit"/>
    </form>
```

#### naver.html에서 검색하면 네이버검색나오게하기

```python
from flask import Flask, render_template
import random
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소

@app.route("/cube/<int:num>")
def cube(num): #메소드에 num 을쓸수있게 함
    triple= num*num*num
    return render_template("soso.html",triple=triple,num=num)#triple과 triple은 다른 개념
    #왼쪽triple은 cube.html에서만 사용가능한 변수
    #오른쪽 triple은 파이썬에서 사용하는 변수
    
@app.route('/lunch')
def lunch():
    menu=["돼지찌게","김치찌게","바보","돈까스"]
    pick = random.choice(menu)
    return render_template("httt.html",menu=pick)
    
@app.route('/rotto')#주소로들어가야 실행됨
def rotto():
    numttt = list(range(1,46))
    a=random.sample(numttt,6)
    s=sorted(a)
    return render_template("too.html",pi=s)
    

@app.route('/naver')
def naver():
    return render_template("naver.html")
    
```

#### naver.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <!--form에 속성명= 속성1을 적는다-->
    <!--쿼리라는 값으로 들어가고 파라미터를 통해 이동시켜준다.-->
    <form action="https://search.naver.com/search.naver?query=">
        <input type="text" name="query"/>
        <input type="submit" value="Submit"/>
    </form>
    
</body>
</html>
```



#### 예제2 구글로 나오게하기

```python
from flask import Flask, render_template
import random
app = Flask(__name__) #app로 변수 저장

@app.route("/") #@넣으면 시작을 정해줌
def hello():#def는 함수 hello를 정의
    return "<h1>안녕하세요</h1>" #안녕하세요를 반환
    
@app.route("/html_tag")#경로를 지정해준다
def html_tag():
    return """
    <h1>첫번째 줄!!!</h1>
    <h2>두번째 줄!!!</h1>
    """
    
#파일띄우기
#flask_intro 폴더안에 templates 폴더를 생성하고
#그안에 html_file.html파일을 생성

@app.route("/html_file")
def html_file():
    return render_template("html_file.html")
    
#templates 폴더안에 welcome.html 파일을 다시만든다.
@app.route("/welcome/<string:name>")#string 이안에 어떤 이름이던 변수로 저장시켜줌
def welcome(name):
    return render_template("welcome.html",people=name)
    
#http://0.0.0.0:8080/ 이주소는 그냥 기본 리턴주소

@app.route("/cube/<int:num>")
def cube(num): #메소드에 num 을쓸수있게 함
    triple= num*num*num
    return render_template("soso.html",triple=triple,num=num)#triple과 triple은 다른 개념
    #왼쪽triple은 cube.html에서만 사용가능한 변수
    #오른쪽 triple은 파이썬에서 사용하는 변수
    
@app.route('/lunch')
def lunch():
    menu=["돼지찌게","김치찌게","바보","돈까스"]
    pick = random.choice(menu)
    return render_template("httt.html",menu=pick)
    
@app.route('/rotto')#주소로들어가야 실행됨
def rotto():
    numttt = list(range(1,46))
    a=random.sample(numttt,6)
    s=sorted(a)
    return render_template("too.html",pi=s)
    

@app.route('/naver')
def naver():
    return render_template("naver.html")
    
@app.route('/google')
def google():
    return render_template("google.html")
```

#### google.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <!--form에 속성명= 속성1을 적는다-->
    <!--쿼리라는 값으로 들어가고 파라미터를 통해 이동시켜준다.-->
    
    <form action="https://www.google.com/search?q="> 
        <input type="text" name="q"/>
        <!--name에 위에 각 홈페이지마다 쿼리 값을 넣어준다-->
        <input type="submit" value="Submit"/>
    </form>
    
</body>
</html>
```

#### github에서 사용하기

명령어

```
cd... #cd..으로 밖으로나오기 
cd email #email로 들어가기
touch .gitignore #gitignore파일 만들기 들어가기 띄어쓰기 조심
git init
git add .
git status #git 상태표시
git rm --cached #잘못올렸을경우 
git log #다시 로그
 git commit -m "email코드 저장하기" #깃에 커밋트 저장하기
```



#### github에 저장하기

```
1.Create a new repository 작성
2.git commit -m "email코드 저장하기" #깃에 커밋트 저장하기
3.홈페이지에 코드 복붙
ex)$ git remote add origin https://github.com/juness99/python_email.git
   $ git push -u origin master
4.Username과 Password 를 치면 됨

```

#### git 서버를 이용하여 TIL 폴더에 넣기

```
cd TIL-junwon
git config --global user.email "wnsdnjs0123@gmail.com"
git config --global user.name "juness99"
git init
git add .
git commit -m "html 너무어려워"
git remote add origin https://github.com/juness99/TIL.git
git push -u origin master
```

