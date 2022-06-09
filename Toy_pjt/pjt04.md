# Pjt 04. 프레임워크를 활용한 웹 페이지 구현



## 목표

- HTML&CSS를 통한 웹 페이지 마크업 및 스타일링 
- Bootstrap 컴포넌트 및 그리드 시스템을 활용한 반응형 레이아웃 구성
- Django web framework를 활용한 웹 서버 구성
- Django Template System을 활용한 웹 페이지 마크업



## 요구사항

영화 추천 서비스 개발을 위한 화면 구성 및 추천 기능 개발 단계로, API를 통해 영화 데이터를 사용할 수 있는 어플리케이션을 완성합니다. 아래 기술된 사항들은 필수적으로 구현해야 하는 내용입니다. django 프로젝트 이름은 pjt04, 앱 이름은 movies로 지정합니다.



## 이번 Pjt를 통해 배운 내용

장고를 이용해 웹 페이지를 구현하는 것을 차근차근 해볼 수 있었습니다.

장고를 배운 며칠간, 부트스트랩과 장고를 함께 사용해보는 경험이 많이 없어서 아쉬웠는데, 이번 프로젝트를 통해 base.html에 부트스트랩을 만들어 놓고 하나하나 디자인하니, html만을 사용할 때보다 훨씬 편하게 프로그래밍 할 수 있다는 것을 느꼈습니다.

장고 자체의 내용을 배우고 이해하는 데에는 앞으로 더 많은 공부가 필요하겠지만, 장고를 잘 활용하게 된다면 제가 원하는 웹 페이지를 보다 효율적으로 개발할 수 있을 것 같습니다.



## 이번 Pjt에서 어려웠던 부분

부트스트랩을 이용하는 건 크게 어렵지 않았지만, api는 거의 기억이 나지 않아 기본 이론을 떠올리고 찾아보는 데에 오랜 시간이 걸렸습니다.

장고의 구조를 아직 제대로 이해하지 못한 것 같습니다. 특히 URL을 다루는 부분이 아직 헷갈립니다. 오늘(03.04) 배운 내용들은 특히 그렇습니다. 응용을 위해서는 더 노력해야 한다는 생각이 들었습니다.



## A. 공유 템플릿 생성 및 사용

### 풀이과정

- 기본적인 장고의 구조를 만들어 놓고 시작했습니다.
- base.html을 만들고, settings에 추가한 다음, index.html과 recommendations.html에 상속했습니다.
- base.html에 부트스트랩 CDN을 추가했습니다.
- 네비게이션 바와 푸터를 pjt03의 내용을 바탕으로 작성했습니다.



### 내가 생각하는 이 문제의 포인트

- 기본적인 장고 어플리케이션 구조 만들기
- base.html을 이용하여 상속하기
- 부트스트랩 CDN가져오기
- 부트스트랩을 이용하여 네비게이션 바와 푸터를 추가하기



## B. 메인 페이지

### 풀이과정

- static 폴더를 만들고 settings에 설정을 추가합니다.
- static 폴더에 원하는 이미지를 추가합니다.
- base.html에 block을 설정하고 index.html에서 block을 활용합니다.
- 이미지를 주어진 명세에 맞게 디자인합니다.
- pjt03의 카드와 헤더를 참고하여 디자인하였습니다.



### 내가 생각하는 이 문제의 포인트

- static 이용하기
- block을 설정하고 상속하여 사용하기
- 부트스트랩을 이용하여 명세에 맞게 디자인하기



## 각 폴더의 코드

### urls.py

```python
from django.contrib import admin
from django.urls import path
from movies import views

app_name = 'movies'
urlpatterns = [
    path('admin/', admin.site.urls),
    path('movies/',views.index, name='index'),
    path('movies/recommendations/',views.recommendations, name='recommendations'),
]
```



### views.py

```python
from django.shortcuts import render

# Create your views here.

def index(request):
    return render(request, 'index.html')

def recommendations(request):
    return render(request, 'recommendations.html')
```



### base.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
</head>


<body>

  {% comment %} 네비게이션 바 {% endcomment %}
  <nav class="navbar navbar-expand-md navbar-dark bg-dark sticky-top d-flex justify-content-between">
    <div class="container-fluid">
      <a class="navbar-brand" href="/movies">SSAFY MOVIE</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" href="/movies">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/movies/recommendations">영화 추천 페이지</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  {% block header %}
  
  {% endblock header %}

  {% block a %}

  {% endblock a %}

  {% comment %} 푸터 {% endcomment %}
  <footer class="fixed-bottom bg-white d-flex justify-content-center align-items-center">
    <ul class="list-unstyled">
      <li>
        <a href="">up</a>
        Django PJT. by youji</li>
    </ul>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>
</html>
```





### index.html

```html
{% extends 'base.html' %}

{% block header %}
{% load static %}
<div class="container">
  <section class="d-flex justify-content-center">
    <img src="{% static 'background.png' %}" class="d-flex justify-content-center my-5" alt="background img">
  </section>
</div>
{% endblock header %}

{% block a %}
<h1 class="d-flex justify-content-center my-7">영화 목록</h1>
<div class="container my-5">
  <section class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4">
    <article class="col">
      <div class="card" style="width: 18rem;">
        <img src="{% static 'a.png' %}" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">???</h5>
          <p class="card-text">장고는 쉽지 않아</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card" style="width: 18rem;">
        <img src="{% static 'b.png' %}" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">할 수 있다</h5>
          <p class="card-text">할 수 있어</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card" style="width: 18rem;">
        <img src="{% static 'c.png' %}" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">주말이다</h5>
          <p class="card-text">주말이야</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card" style="width: 18rem;">
        <img src="{% static 'd.png' %}" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">관통 프로젝트에</h5>
          <p class="card-text">관통당했어요</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card" style="width: 18rem;">
        <img src="{% static 'e.jpg' %}" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">반짝반짝</h5>
          <p class="card-text">반짝반짝</p>
        </div>
      </div>
    </article class="col">
    <article>
      <div class="card" style="width: 18rem;">
        <img src="{% static 'thatsyou.png' %}" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">빛</h5>
          <p class="card-text">그 빛이 너였구나</p>
        </div>
      </div>
    </article>
  </section>
</div>
{% endblock a %}
```

