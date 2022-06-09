# pjt 06. 



## 목표

- 데이터를 생성, 조회, 수정, 삭제할 수 있는 Web application 제작
- Django web framework를 통한 데이터 조작
- ORM(Object Relational Mapping)에 대한 이해
- Django ModelForm을 활용한 사용자 요청 데이터 유효성 검증



## 요구사항

커뮤니티 서비스의 게시판 기능 개발을 위한 단계로, 영화 데이터의 생성, 조회, 수정, 삭제 가능 한 어플리케이션을 완성합니다. 해당 기능은 향후 커뮤니티 서비스의 필수 기능으로 사용됩니다. 아래 기술된 사항들은 필수적으로 구현해야 하는 내용입니다. Django 프로젝트 이름은 pjt06, 앱 이름은 movies로 지정합니다.



## 이번 PJT 에서 배운 내용

- HTTP requests를 다루는 법
- 미디어 파일을 업로드하고 resizing 하는 법
- modelform 사용하는 법
- crud를 이용하여 form을 사용하는 법
- migrations에 문제가 생겼을 때 해결하는 법
- 에러 메세지를 보고 문제를 해결하는 법



## 이번 PJT에서 어려웠던 부분

- 프로젝트와 앱을 만들고 구성하는 건 어렵지 않았으나, model을 수정하고 migrations, migrate하는 과정에서 오류가 생겨서 해결하는 게 쉽지 않았다.
- 부트스트랩 카드를 이용해서 detail 화면을 구성할 때 원하는 자료가 원하는 형태로 보여지지 않았다. 그 이유를 탐색하니 create에서부터 문제가 생기는 것으로 보였다.
- 하나의 수정사항이 발생하면 많은 파일에서 변경해야 한다는 게 번거롭고, 오류가 나는 부분을 모두 찾는 게 쉽지 않았다.



## A. 공유 템플릿

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
  <title>Document</title>
</head>
<body>
  <div class="container">
    {% block content %}
    {% endblock content %}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>
</html>
```

이전에 하던 거의 그대로 사용해서 별다른 문제가 없었다.



## B. 전체 영화 조회 템플릿 (index.html)

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Movies</h1>
  <a href="{% url 'movies:create' %}">CREATE</a>
  <hr>
  {% for movie in movies %}
    <a href="{% url 'movies:detail' movie.pk %}">{{ movie.title }}</a>
    <p></p>
    <p>{{ movie.score }}</p>
    <hr>
  {% endfor %}
{% endblock content %}
```

1. base.html을 extends했다.
2. block을 만들고, CREATE 버튼을 만들었다.
3. movies 안을 순회하는 movie를 만들고, movie.title에 연결되는 a태그를 설정해 주었다.
4. 명세와 같이 score 값을 아래에 표시했다.



## C. 영화 상세 정보 페이지(detail.html)

```html
{% extends 'base.html' %}

{% block content %}
  <h1>DETAIL</h1>
  <div class="card" style="width: 20rem;">
    {% if movie.image %}
      <img src="{{ movie.image.url }}" alt="{{ movie.image }}">
    {% endif %}
    <div class="card-body">
      <h5 class="card-title">{{ movie.title }}</h5>
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item">장르 : {{ movie.genre }}</li>
      <li class="list-group-item">평점 : {{ movie.score }}</li>
      <p class="card-text">{{ movie.description }}</p>
    </ul>
    <div class="card-body">
      <a href="{% url 'movies:update' movie.pk %}">수정</a>
      <form action="{% url 'movies:delete' movie.pk %}" method="POST">
        {% csrf_token %}
        <input type="submit" value="삭제">
      </form>
      <a href="{% url 'movies:index' %}">back</a>
    </div>
  </div>
{% endblock content %}
```

1. base.html을 extends했다.
2. 처음에는 기본 html로 구현하기 시작했다. 이 때, model에 필요한 속성이 부족하다는 것을 깨달았다.
3. model을 수정하면서 에러 메세지가 생기고 문제가 다수 발생하였다.
4. db를 지우고 다시 migrations를 진행하였다.
5. 기본 html로 구현한 