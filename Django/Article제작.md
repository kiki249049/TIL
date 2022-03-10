# 03-10 WorkShop

articles/urls.py

```python
from django.urls import path
from . import views

app_name='articles'
urlpatterns = [
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'),
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/delete/', views.delete, name='delete'),
    path('<int:pk>/edit/', views.edit, name='edit'),
    path('<int:pk>/update/', views.update, name='update'),
]

```

articles/views.py

```python
from django.shortcuts import render, redirect
from .models import Article

def index(request) :
    articles= Article.objects.all()[::-1]
    context = {
        'articles' : articles,
    }
    return render(request, 'articles/index.html', context)

def new(request) :
    return render(request, 'articles/new.html')

def create(request) :
    title = request.POST.get('title')
    content = request.POST.get('content')
    article = Article(title=title, content=content)
    article.save()
    return redirect('articles:detail', article.pk)

def detail(request, pk) :
    article = Article.objects.get(pk=pk)
    context={
        'article' : article,
    }
    return render(request, 'articles/detail.html', context)

def delete(request, pk) :
    article = Article.objects.get(pk=pk)
    if request.method == 'POST' :
        article.delete()
        return redirect('articles:index')
    else :
        return redirect('articles:detail', article.pk)

def edit(request,pk) :
    article = Article.objects.get(pk=pk)
    context = {
        'article' : article,
    }
    return render(request, 'articles/edit.html', context)

def update(request, pk) :
    article = Article.objects.get(pk=pk)
    article.title = request.POST.get('title')
    article.content = request.POST.get('content')
    article.save()
    return redirect('articles:detail', article.pk)
```

templates/articles의 html 들

```django
create.html
{% extends 'base.html' %}

{% block content %}
  <h1 class="text-center">성공적으로 글이 작성되었습니다.</h1>
{% endblock content %}

detail.html
{% extends 'base.html' %}
{% block content %}
  <h2 class="text-center">DETAIL</h2>
  <h3>{{ article.pk }}번째</h3>
  <hr>
  <p>제목 : {{ article.title }}</p>
  <p>내용 : {{ article.content }}</p>
  <p>작성 시각 : {{ article.created_at }}</p>
  <p>수정 시각 : {{ article.updated_at }}</p>
  <hr>
  <a href="{% url 'articles:edit' article.pk %}" class='btn btn-primary'>EDIT</a><br>
  <form action="{% url 'articles:delete' article.pk %}" method="POST">
    {% csrf_token %}
    <button class='btn btn-danger'>DELETE</button>
  </form>
  <a href="{% url 'articles:index' %}">[BACK]</a>
{% endblock content %}

edit.html
{% extends 'base.html' %}
{% block content %}
  <h1 class="text-center">EDIT</h1>
  <form action="{% url "articles:update" article.pk %}" method="POST">
    {% csrf_token %}
    <label for="title">TITLE : </label>
    <input type="text" name='title' id='title' value="{{ article.title }}"><br>
    <label for="content">CONTENT</label>
    <textarea name="content" id="content" cols="30" rows="10">{{ article.content }}</textarea><br>
    <input type="submit">
  </form>
  <br>
  <a href="{% url 'articles:index' %}">[BACK]</a>
{% endblock content %}

index.html
{% extends 'base.html' %}

{% block content %}
  <h1 class="text-center">Articles</h1>
  <a href="{% url 'articles:new' %}">NEW</a>
  <hr>
  {% for article in articles  %}
    <p>글 번호 : {{ article.pk }}</p>
    <p>글 제목 : {{ article.title }}</p>
    <p>글 내용 : {{ article.content }}</p>
    <a href="{% url 'articles:detail' article.pk %}">[detail]</a>
    <hr>
  {% endfor %}
{% endblock content %}

new.html
{% extends 'base.html' %}
{% block content %}
  <h1 class="text-center">NEW</h1>
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    <label for="title">TITLE : </label>
    <input type="text" name='title' id='title'><br>
    <label for="content">CONTENT</label>
    <textarea name="content" id="content" cols="30" rows="10"></textarea><br>
    <input type="submit">
  </form>
  <br>
  <a href="{% url 'articles:index' %}">[BACK]</a>
{% endblock content %}
```

![image-20220310180519957](https://user-images.githubusercontent.com/97595340/157628296-9c03bd4d-0cc0-40c4-a7c7-12747ac326aa.png)

![image-20220310180529817](https://user-images.githubusercontent.com/97595340/157628307-f1b25805-677f-44fd-8a80-c5e72ef3b4cc.png)

![image-20220310180549159](https://user-images.githubusercontent.com/97595340/157628320-9cf2996d-af73-4971-9f65-5c8006bfaed3.png)

![image-20220310180602099](https://user-images.githubusercontent.com/97595340/157628328-ff6fd6a2-0b00-4683-976a-74eccd0f1330.png)