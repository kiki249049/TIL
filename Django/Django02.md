### Model

단일한 데이터에 대한 정보를 가짐

저장된 데이터베이스의 구조

장고 모델을 통해 데이터에 접속하고 관리

일반적으로 각각의 모델은 하나의 DB테이블에 매핑

### Database

db  : 체계화된 데이터의 모임

query : 데이터를 조회하기 위한 명령어

스키마 : 자료의 구조, 표현방법, 관계등을 정의한 구조

테이블 : 열(필드,속성) , 행(레코드,튜플)

pk : primary key(기본키) 각 행의 고유값으로 primary key로 불린다. 반드시 설정하여야하고 관계 설정시 주요하게 활용된다.

### ORM

파이썬언어를 sql문으로 바꿔주는 프로그램 객체지향 프로그래밍과 RDBMS를 연동할때 쓰인다. 장고는 내장 장고orm을 쓴다.

```python
class Article(models.Model) :
    title = models.CharField(max_length=10)
    content = models.TextField()
```

### Django Field

1. CharField

```python
CharField(max_length=None, **options)
```

길이의 제한이 있는 문자열을 넣을때 사용

2.  TextField

```python
TextField()
```

글자의 수가 많을 때 사용

max_length 적용시 textarea 위젯에 반영은 되지만 모델과 데이터베이스 수준에는 적용 x

### Migration

: 장고가 모델에 생긴 변화는 반영하는 방법

1. Makemigrations

model을 변경한 것에 기반한 새로운 마이그레이션을 만들때 사용

1. migrate

마이그레이션을 db에 반영하기 위해 사용

설계도를 db에 반영하는 과정

모델에서의 변경사항들과 db의 스키마가 동기화를 이룸

1. sqlmigrate

마이그레이션에 대한 sql구문을 보기 위해 사용

마이그레이션이 sql문으로 어떻게 해석되어서 동작할지 미리 확인

1. showmirgrations

프로젝트 전체의 마이그레이션 상태를 확인하기 위해 사용

```shell
$ python manage.py makemigrations
```

migrations/0001_initial.py 을 통해 생성확인

```shell
$ python manage.py migrate
```

sqlmigrate

```shell
$ python manage.py sqlmigrate app_name 0001
```

model 수정

```python
created_at = models.DateTimeField(auto_now_add=True)
updated_at = models.DateTimeField(auto_now=True)
```

created_at 필드에 default값 1설정

auto_now_add : 최초 생성 일자

auto_now : 최초 수정 일자

```shell
Article.objects.all()
```

QuerySet

: 데이터베이스로부터 전달받은 객체 목록

일반 shell로는 장고 프로젝트 환경에 접근을 하지 못하고 장고shell로만 접근가능

ipython과 django-extensions 설치

```python
INSTALLED_APPS = [
    'django_extensions'
]
```

설치앱에 장고 익스텐션을 추가

```shell
$ python manage.py shell_plus
```

## CRUD

Createm Read, Update, Delete를 묶어서 부르는 말

### READ

```shell
Article.objects.all()
<QuerySet []>
```

레코드가 하나면 있으면 인스턴스 객체로, 두 개이상이면 쿼리셋으로 리턴

### article 생성방법1

```powershell
aricle = Article()
article.title = "title"
article.content = "content"
article.save()
Article.objects.all()
```

### article 생성방법2

```powershell
article = Article(title='title', content='content')
article.save()
```

### article 생성방법3

```powershell
Article.objects.create(title='title', content='content')
```