# Pjt 05. 프레임워크 기반 웹 페이지 구현



## 목표

- 데이터를 생성, 조회, 수정, 삭제할 수 있는 Web application 제작
- Django web framework를 통한 데이터 조작
- ORM(Object Relational Mapping)에 대한 이해 
- 관리자 페이지를 통한 데이터 관리



## 요구사항

커뮤니티 서비스의 게시판 기능 개발을 위한 단계로, 영화 데이터의 생성, 조회, 수정, 삭제 가능 한 어플리케이션을 완성합니다. 해당 기능은 향후 커뮤니티 서비스의 필수 기능으로 사용됩니다. 아래 기술된 사항들은 필수적으로 구현해야 하는 내용입니다. django 프로젝트 이름은 pjt05, 앱 이름은 movies로 지정합니다.



## 이번 Pjt를 통해 배운 내용

- model과 cdrn을 사용하여 게시판을 구성할 수 있게 되었습니다.



## 이번 Pjt에서 어려웠던 부분

- db를 다루는 부분에서 잦은 오류가 발생하여 어려움을 겪었습니다.
- 사용하는 필드의 개수가 늘어나면서 놓치는 필드가 생기거나 오탈자가 발생하는 경우가 있었습니다.
- new와 create, edit와 update의 관계와 같은 view 함수의 관계를 이해하기 쉽지 않았습니다.



---



## A. 공유 템플릿(base.html)



### 풀이과정

- 가상환경과 requirements.txt 설치, 기본 틀 제작을 먼저 하였습니다.
- base.html과 templates, settings 작성을 완료했습니다.
- 장고 필드를 확인하며 admin, models를 작성하였습니다.
- migrations을 만들고 db에 반영하였습니다.
- CDRN에 맞추어 urls, views, templates를 작성하였습니다.



### 내가 생각하는 이 문제의 포인트

- 기본적인 장고 프로젝트 제작 방법을 아는 것
- admin, models를 필요한 필드를 사용하여 작성하는 것
- migration을 이용하여 db와 연결하고 확인하는 것
- CDRN에 맞추어 기본 틀을 제작하는 것



---



## B. 전체 영화 목록 조회 템플릿 (index.html)



### 풀이과정

- urls > views > index.html 순으로 작성하였습니다.



### 내가 생각하는 이 문제의 포인트

- 원하는 방향으로 링크가 작동하도록 url 작성하기
- a태그를 사용하여 링크를 만들고, 적절한 url 넣기
- for 문을 이용하여 title을 모두 보여주기
- class Movie를 이용해 db의 정보 불러오기



---



## C. 영화 상세 정보 페이지 (detail.html)



### 풀이과정

- urls > views > detail.html 순으로 작성하였습니다.



### 내가 생각하는 이 문제의 포인트

- db에서 각자 영화의 pk값을 가져와서 이용하는 view함수 작성하기
- img 태그를 이용하여 poster가 보일 수 있게 작성하기
- button을 이용하여 이동할 수 있는 링크 작성하기
-  csrf_token 사용하기



---



## D. 영화 작성 페이지 (new.html)



### 풀이과정

- urls > views > new.html 순으로 작성하였습니다.



### 내가 생각하는 이 문제의 포인트

- new와 create를 구별하여 view 함수를 작성하고 그 흐름 이해하기
- select를 이용하여 장르를 선택할 수 있도록 하기
- 정보를 받고 저장하는 함수 작성하기



---



## E. 영화 수정 페이지 (edit.html)



### 풀이과정

- urls > views > edit.html 순으로 작성하였습니다.



### 내가 생각하는 이 문제의 포인트

- edit와 update를 구별하여 view 함수를 작성하고 그 흐름 이해하기
- 정보를 전달받고 변경하는 함수 작성하기



----



## 작성한 코드



### urls.py

```python 
from django.urls import path
from . import views

app_name = 'movies'
urlpatterns = [
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'),
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/delete', views.delete, name='delete'),
    path('<int:pk>/edit', views.edit, name='edit'),
    path('<int:pk>/update', views.update, name='update'),
]
```



### view.py

```python
from django.shortcuts import redirect, render
from .models import Movie

# Create your views here.

def index(request):
    movies = Movie.objects.all()[::-1]
    context = {
        'movies' : movies,
    }
    return render(request, 'movies/index.html', context)



def new(request):

    return render(request, 'movies/new.html')



def create(request):
    title = request.POST.get('title')
    audience = request.POST.get('audience')
    release_date = request.POST.get('release_date')
    genre = request.POST.get('genre')
    score = request.POST.get('score')
    poster_url = request.POST.get('poster_url')
    content = request.POST.get('content')
    
    movie = Movie()
    movie.title = title
    movie.audience = audience
    movie.release_date = release_date
    movie.genre = genre
    movie.poster_url = poster_url
    movie.score = score
    movie.content = content
    movie.save()
    return redirect('movies:detail', movie.pk)



def detail(request, pk):
    movie = Movie.objects.get(pk=pk)
    context = {
        'movie' : movie,
    }
    return render(request, 'movies/detail.html', context)



def edit(request, pk):
    movie = Movie.objects.get(pk=pk)
    context = {
        'movie' : movie,
    }
    return render(request, 'movies/edit.html', context)



def update(request, pk):
    movie = Movie.objects.get(pk=pk)
    if request.method == "POST":
        movie.title = request.POST.get('title')
        movie.audience = request.POST.get('audience')
        movie.release_date = request.POST.get('release_date')
        movie.genre = request.POST.get('genre')
        movie.score = request.POST.get('score')
        movie.poster_url = request.POST.get('poster_url')
        movie.content = request.POST.get('content')
        movie.save()
    return redirect('movies:detail', movie.pk)



def delete(request, pk):
    movie = Movie.objects.get(pk=pk)
    if request.method == "POST":
        movie.delete()
        return redirect('movies:index')
    else:
        return redirect('movies:detail', movie.pk)
```



### models.py

```python
from django.db import models

# Create your models here.
class Movie(models.Model):
    title = models.CharField(max_length=30)
    audience = models.IntegerField()
    release_date = models.DateField()
    genre = models.CharField(max_length=10)
    score = models.FloatField()
    poster_url = models.TextField()
    content = models.TextField()
```



### admin.py

```python
from django.contrib import admin
from .models import Movie
# Register your models here.


class MoviesAdmin(admin.ModelAdmin):
    list_display = ('title', 'audience', 'release_date',
     'genre','score','poster_url', 'content', 'pk',)

admin.site.register(Movie,MoviesAdmin)
```



### index.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>INDEX</h1>
  
  <a href="{% url 'movies:new' %}">NEW</a>
  <hr>
  {% for movie in movies %}
    
    <a href="{% url 'movies:detail' movie.pk %} ">{{ movie.title }}</a>
    <p>{{ movie.score }}</p>

    <hr>
  {% endfor %}

{% endblock content %}
```



### detail.html

```html
{% extends 'base.html' %}

{% block content %}
<h1>DETAIL</h1>


<hr>
<img src="{{ movie.poster_url }}" alt="#" width="400" class="img-responsive center-block">
<h3>{{ movie.title }}</h3>

<p>Audience : {{ movie.audience }}</p>
<p>Release Dates : {{ movie.release_date }}</p>
<p>Genre : {{ movie.genre }}</p>
<p>Score : {{ movie.score }}</p>
<p>{{ movie.content }}</p>
<hr>

<div class='container'>
  <div class="row">
    <a href="{% url 'movies:edit' movie.pk %}">EDIT</a>
    <form action="{% url 'movies:delete' movie.pk %}" method="POST">
      {% csrf_token %}
      <button class='btn btn-link p-0'>DELETE</button>
    </form>
    <br>

    <a href="{% url 'movies:index' %}">BACK</a>
  </div>
</div>



{% endblock content %}
```



### new.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>New</h1>

  <form action="{% url 'movies:create' %}" method="POST">
    {% csrf_token %}
    <label for="title">TITLE :</label>
    <input type="text" name="title" id="title"><br>

    <label for="audience">AUDIENCE :</label>
    <input type="integer" name="audience" id="audience"><br>

    <label for="release_date">RELEASE_DATES :</label>
    <input type="date" name="release_date" id="release_date"><br>

    <label for="genre">GENRE :</label>
      <select name="genre" id="genre">
        <option value="판타지">판타지</option>
        <option value="액션">액션</option>
        <option value="로맨스">로맨스</option>
        <option value="공포">공포</option>
        <option value="스릴러">스릴러</option>
      </select><br>

    <label for="score">SCORE :</label>
    <input type="float" name="score" id="score"><br>

    <label for="poster_url">POSTER_URL :</label>
    <input type="text" name="poster_url" id="poster_url"><br>

    <label for="content">CONTENT :</label>
    <textarea name="content" id="content" cols="30" rows="10"></textarea><br>
    

    <input type="submit"><br>
    <a href="{% url 'movies:index' %}">BACK</a>
  </form>

{% endblock content %}
```



### edit.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>EDIT</h1>

  <form action="{% url 'movies:update' movie.pk %}" method="POST">
    {% csrf_token %}

    <label for="title">TITLE :</label>
    <input type="text" name="title" id="title" value="{{ movie.title }}"><br>

    <label for="audience">AUDIENCE :</label>
    <input type="integer" name="audience" id="audience" value="{{ movie.audience }}"><br>

    <label for="release_date">RELEASE_DATES :</label>
    <input type="date" name="release_date" id="release_date" value="{{ movie.release_date | date:"Y-m-d" }}"><br>

    <label for="genre">GENRE :</label>
      <select name="genre" id="genre">
        <option value="판타지">판타지</option>
        <option value="액션">액션</option>
        <option value="로맨스">로맨스</option>
        <option value="공포">공포</option>
        <option value="스릴러">스릴러</option>
      </select><br>

    <label for="score">SCORE :</label>
    <input type="float" name="score" id="score" value="{{ movie.score }}"><br>

    <label for="poster_url">POSTER_URL :</label>
    <input type="text" name="poster_url" id="poster_url" value="{{ movie.poster_url }}"><br>

    <label for="content">CONTENT :</label>
    <textarea name="content" id="content" cols="30" rows="10" value="{{ movie.content }}"></textarea><br>
    

    <input type="submit"><br>
    <a href="{% url 'movies:index' %}">BACK</a>
  </form>

{% endblock content %}
```



---



## 화면 사진

![image-20220311185437485](Pjt%2005.%20%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%20%EA%B8%B0%EB%B0%98%20%EC%9B%B9%20%ED%8E%98%EC%9D%B4%EC%A7%80%20%EA%B5%AC%ED%98%84.assets/image-20220311185437485.png)



![image-20220311185449684](Pjt%2005.%20%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%20%EA%B8%B0%EB%B0%98%20%EC%9B%B9%20%ED%8E%98%EC%9D%B4%EC%A7%80%20%EA%B5%AC%ED%98%84.assets/image-20220311185449684.png)



![image-20220311185509216](Pjt%2005.%20%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%20%EA%B8%B0%EB%B0%98%20%EC%9B%B9%20%ED%8E%98%EC%9D%B4%EC%A7%80%20%EA%B5%AC%ED%98%84.assets/image-20220311185509216.png)

![image-20220311185521280](Pjt%2005.%20%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%20%EA%B8%B0%EB%B0%98%20%EC%9B%B9%20%ED%8E%98%EC%9D%B4%EC%A7%80%20%EA%B5%AC%ED%98%84.assets/image-20220311185521280.png)