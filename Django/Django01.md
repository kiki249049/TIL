# Django01

### MTV 구조

Model : 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리

Templates : 파일의 구조나 레이아웃을 정의

View : http요청을 수신하고 응답을 반환(view함수를 통해)

### 프로젝트 생성

```shell
$ django-admin startproject firstpjt .
```

### 서버 시작하기

```shell
$ python manage.py runserver
```

장고버전은 LTS(장기지원버전)인 3.2.12버전을 깔아준다.

### 프로젝트 구조

__init__ : python에게 이 디렉토리를 하나의 python 패키지로 다루도록 지시

asgi : 장고 애플리케이션이 비동기식 웹서버와 연결 및 소통

settings : 애플리케이션의 모든 설정을 포함

urls : 사이트의 url과 적절한 views의 연결을 지정

wsgi : 장고의 어플리케이션이 웹서버와 연결 및 소통하는 것을 도움

---------------

manage.py : 장고 프로젝트와 다양한 방법으로 상호작용하는 유틸리티

### 어플리케이션 생성

```shell
$ python manage.py startapp app_name
```

### 어플리케이션 구조

admin.py : 관리자용 페이지를 설정하는 곳

apps.py : 앱의 정보가 작성된 곳

models.py : 앱에서 사용하는 model을 정의하는곳

tests.py : 프로젝트의 테스트 코드를 작성하는 곳

views.py : view 함수들이 정의 되는 곳

### 앱 등록

프로젝트 폴더에서 INSTALLED_APPS 리스트에 어플리케이션을 추가해준다. (반드시 생성 후 등록!)

권장사항 : local apps , Third party apps, Django.apps 순으로 등록하는 것을 권장

## 요청과 응답

### URLs

: urlspatterns 리스트에 path를 만들어준다.

```python
urlpatterns = [
	path('admin/', admin.site.urls),
	path('index/', views.index),
]
```

### Views

view함수를 정의하는 부분

### Templates

실제 내용을 보여주는데 사용되는 파일 django.html파일이 저장돼있다.

### 언어 설정 방법

:settings.py에 들어가서 LANGUAGE_CODE를 ko-kr과 TIME_ZONE을 Asia/Seoul로 바꿔준다.

이 설정이 적용되려면 USE_I18N이 활성화 돼있어야한다.(language_code)

Time_zone을 활성화 시킬려면 USE_TZ가 True여야한다.

### 추가설정

USE_I18N : 장고의 번역 시스템을 활성화 해야 하는지 여부를 지정

USE_L10N : 데이터의 지역화된 형식을 기본적으로 활성화할지 여부를 지정

USE_TZ : datetimes가 기본적으로 시간대를 인식하는지 여부를 지정

## Template

### DTL

1. Variable

: render()를 사용하여 views.py에서 정의한 변수를 template 파일로 넘겨 사용하는것

render의 세번쨰 인자로 {'key' : value} 와 같이 넘겨주게 된다.

2. filter

```django
{{ variable|filter }}
{{ variable|lower }}
{{ variable|truncatewords:30 }} # 30단어 까지만 보여줌
```

표시할 변수를 수정할 떄 사용

3. tag

```django
{{% tag %}}
# ex) {{% if %}}{{% endif %}}
```

4. comment

```django
{{% comment %}}

{{% endcomment %}}
```

: 주석의 역할을 한다.

## 항상 코드 작성 순서는 urls - view - templates 순서로 한다

### include tag

: 상위에 templates 폴더를 만들어 BASE_DIR에 추가 해줘 base.html을 스켈레톤 코드로 사용할 수 있찌만 include tag를 이용해 base.html 뿐만 아니라 다른 html파일도 렌더링 할 수 있다.



### 장고의 설계 철학

: 로직과(view) 표현(templates)은 분리 되어야한다.



## HTML FORM

### HTML "form" element

: 웹에서 사용자 정보를 입력하는 여러방식(text, button, checkbox..등)을 제공하고 사용자로부터 할당된 데이터를 **서버로 전송하는 역할**  

#### 핵심속성

1. action : 입력된 데이터가 전송될 URL 지정
2. method : 입력 데이터 전달 방식 지정

### HTML "input" element

```django
<input name="name">
```

값을 넘길때 name이라는 변수에 저장해서 넘김

### HTML "label" element

: 사용자 인터페이스 항목에 대한 설명을 나타냄

label과 input을 연결하기 위해선 input의 id값과 label의 **for값**이 일치해야한다.

#### label과 연결할 수 있는 요소

ex) button, input, textarea, select

### HTTP request method "GET" 

: 서버로부터 정보를 조회하는데 사용

## URL

### Variable Routing

```python
path('account/user/<int:user_pk>/')
```

1. str : 문자열
2. int : 숫자
3. slug : 아스키 문자 또는 숫자, 하이픈 및 밑줄문자로 구성된 모든 슬러그 문자열과 매치

### Naming URL patterns

```python
path('index/', views.index, name='index'),을
html파일에서
<a href="{{% url="index" %}}">메인페이지</a>로 연결가능하다.
```



### Framework의 성격

1. opinionated 독선적 -> Django!

   