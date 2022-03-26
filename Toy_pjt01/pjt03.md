# Pjt 03. 반응형 웹 페이지 구성



## 목표

- HTML을 통한 웹 페이지 마크업 분석
- CSS 라이브러리 이해와 활용
- 컴포넌트 및 그리드 시스템 활용
- 커뮤니티 서비스 반응형 레이아웃 구성



## 요구사항

커뮤니티 서비스 개발을 위한 화면 구성 단계로, 유저가 보는 프론트 엔드를 개발합니다.



## 이번 Pjt를 통해 배운 내용

bootstrap의 components 기능을 사용하는 법

components의 코드를 copy해온 후, 원하는 내용을 원하는 장소에 삽입 또는 대체하는 법

class 선언을 하는 위치를 선정하는 법 (아직 50% 정도 진행 중)

웹 페이지에 반응형 카드를 구성하는 법

카드가 아닌 표를 반응형으로 구성하면서, d-none을 사용하는 법

html의 문법 (아직 50% 정도 진행 중)

css를 곁들이는 법 (아직 css 30% 정도 진행 중)



## A. nav_footer



### 풀이과정

이전에 사용했던 실습 파일을 참고하여 네비게이션 바를 만들었다.

처음에 bootstrap 공식 문서의 navbar navbar-expand-md가 창을 줄이면 햄버거 모양이 뜬다는 것을 모르는 채로 기본 navbar에서 작업하다가, 햄버거 모양이 항상 있는 navbar 코드를 카피해 와서 창을 키웠을 때 햄버거 모양이 사라지게 하려고 했다. (소위 삽질을 했다.)

이후에 navbar-expand-md가 창을 줄이면 햄버거 모양이 뜬다는 것을 알고, 코드를 카피해 와서 다시 처음부터 진행하였다. 꼭 창을 줄이는 행동이 아니더라도, 코드를 읽었을 때 어떤 속성들이 포함되어 있는지 대략적으로나마 아는 능력을 갖추고 있었다면 이런 실수는 없었을 것이다. bootstrap에서 코드를 그냥 카피해 오는 것이 대수가 아니라는 것을 크게 느꼈다.

이후 a링크를 생성하거나, active를 주거나, 색상 등의 속성을 만드는 것은 크게 어렵지 않았다.

다만, 로고 크기가 너무 커서 이미지 수정이 필요해서 css에 height 속성을 추가하였다. 추가한 후 확인해 보니 네비게이션 바가 너무 뚱뚱해서 width로 바꾸어서 로고 크기를 조금 작게 만들었다.

fixed-top보다 sticky-top이 바람직하다고 느꼈다. 하단에 이미지가 삽입될 것이기 때문이다. 같은 이유로, A번 코드에 footer는 fixed-bottom으로 설정되어 있으나 이후 B, C에서 sticky-bottom으로 변경하였다.

이후에 modal과 form 코드를 copy 해서 login 에 연결하고 form을 삽입하였다.

footer에 클래스를 부여하고, 제작하였다.



```html
  <!-- 01_nav_footer.html -->
  <nav class="navbar navbar-expand-md navbar-dark bg-dark sticky-top d-flex justify-content-between">
    <div class="container-fluid">
      <a href="02_home.html" class="navbar-brand">
        <img src="images/logo.png" alt="로고">
      </a>
      <div>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" 
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="02_home.html"><d>Home</d></a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="03_community.html">Community</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" data-bs-toggle="modal" data-bs-target="#exampleModal">Login</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </nav>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <form>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Email address</label>
          <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
          <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label">Password</label>
          <input type="password" class="form-control" id="exampleInputPassword1">
        </div>
        <div class="mb-3 form-check">
          <input type="checkbox" class="form-check-input" id="exampleCheck1">
          <label class="form-check-label" for="exampleCheck1">Check me out</label>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
  </div>
</div>
  
  <footer class="fixed-bottom bg-white d-flex justify-content-center align-items-center">
    <ul class="list-unstyled">
      <li>Web-bootstrap PJT. by youji</li>
    </ul>
  </footer>
```





### 이 문제에서 어려웠던 점

햄버거를 가지고 삽질한 것이 정신적으로 어려웠다.

색상이나 폰트와 같은 속성은 이전에 한 경험 덕분에 크게 어렵지 않았다. 다만 아직 container-fluid 클래스와 container가 정확히 어떤 역할을 하고 있는지 완벽히 이해하지 못했다. 이 부분은 더 공부해야겠다.

또한 각각 로고, 리스트 등등의 위치를 선언하는 것이 크게 어렵지는 않았으나, 반복적으로 하는 것이지 완벽하게 이해하고 사용하지 않는다고 느껴져서 공부가 더 필요하다는 생각이 들었다. 개구리 게임을 여러 번 해보아야겠다.

modal 코드를 copy해 와서 login에 연결하는 것이 어려웠다. 또한 modal 코드의 일정 부분을 form으로 변환하는 것도 쉽지 않았다. 풀이 과정에서 이야기했던 '코드를 읽는 능력' 이 필요하다고 다시 느껴진 부분이다.



### 내가 생각하는 이 문제의 포인트

bootstrap에서 코드를 copy해 왔을 때 적절한 부분을 대체하고, 필요한 곳에 연결하는 법 익히기

여러 가지 태그 사용하는 법 익히기

여러 가지 클래스 사용하는 법 익히기





## B. 02_home



### 풀이과정

bootstrap에서 carousel의 코드를 copy하고, 붙여넣어서 요구사항을 덧붙여 구성했다.

boxoffice를 원하는 위치에 원하는 스타일로 꾸미고,

필요로 하는 card 디자인을 가지고 와서 불필요한 코드는 지우고 카드 모양을 구성하였다.
그리고 section에 클래스를 선언하여 grid로 만들어 주었다.



```html

  <!-- 02_home.html -->
  <header>
    <div id="carouselExampleSlidesOnly" class="carousel slide" data-bs-ride="carousel">
      <div class="carousel-inner">
        <div class="carousel-item active">
          <img src="images/header1.jpg" class="d-block w-100" alt="헤더 이미지1">
        </div>
        <div class="carousel-item">
          <img src="images/header2.jpg" class="d-block w-100" alt="헤더 이미지2">
        </div>
        <div class="carousel-item">
          <img src="images/header3.jpg" class="d-block w-100" alt="헤더 이미지3">
        </div>
      </div>
    </div>

  </header>

  <h1 class="d-flex justify-content-center my-5">Boxoffice</h1>
  <div class="container">
    <section class="row row-cols-1 row-cols-md-3 g-4">
      <article class="col">
        <div class="card" style="width: 18rem;">
          <img src="images/movie1.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </article>
      <article class="col">
        <div class="card" style="width: 18rem;">
          <img src="images/movie2.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </article>
      <article class="col">
        <div class="card" style="width: 18rem;">
          <img src="images/movie3.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </article>
      <article class="col">
        <div class="card" style="width: 18rem;">
          <img src="images/movie4.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </article>
      <article class="col">
        <div class="card" style="width: 18rem;">
          <img src="images/movie5.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </article class="col">
      <article>
        <div class="card" style="width: 18rem;">
          <img src="images/movie6.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </article>
    </section>
  </div>
```





### 이 문제에서 어려웠던 점

section과 article에 class를 각각 어떻게 넣어야 원하는 방식으로 작동하는지 이해하기 어려웠다.

아직까지 정확히 어떤 곳에 어떤 class를 부여해야 하는지 명확하게 알지 못한다.



### 내가 생각하는 이 문제의 포인트

gird 구현하기

carosel 컴포넌트 구성하기







## C. 03_community



### 풀이과정

게시판 목록인 aside를 list gruop 코드를 copy 해와서 구성했다.

grid로 구성하기 위해 div class row를 바깥에 선언하고 sidebar의 gird를 선언해 주었다.

board를 table 중 가장 가까운 스타일로 copy 해온 후, 요구사항에 맞춰 행과 열을 구성했다.

마지막으로 article을 list group 코드를 바탕으로 구성한 다음, table과 article을 gird로 변환할 수 있게끔 d-block, d-lg-none을 이용하였다.

paginator을 구성한 다음 게시판 아래, 중앙에 위치하였다.



```html
  <!-- 03_community.html -->
  <div class="main container">
    <h1 class="d-flex justify-content-center my-5">Community</h1>
    <div class="row">
    <!-- Sidebar -->
      <aside class="col-12 col-lg-2">
        <ul class="list-group">
          <li class="list-group-item"><a href="#" style="text-decoration:none">Boxoffice</a></li>
          <li class="list-group-item"><a href="#" style="text-decoration:none">Movies</a></li>
          <li class="list-group-item"><a href="#" style="text-decoration:none">Genres</a></li>
          <li class="list-group-item"><a href="#" style="text-decoration:none">Actors</a></li>
        </ul>
      </aside>
    

    <!-- Board -->
    <section class="col-12 col-lg-10">
      <div class="d-none d-lg-block">
        <table class="table table-striped">
          <thead class="bg-dark text-white">
            <tr>
              <th scope="col">영화 제목</th>
              <th scope="col">글 제목</th>
              <th scope="col">작성자</th>
              <th scope="col">작성 시간</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Great Movie title</th>
              <td>Movie Test</td>
              <td>youji</td>
              <td>1 minutes ago</td>
            </tr>
            <tr>
              <th scope="row">Great Movie title</th>
              <td>Movie Test</td>
              <td>youji</td>
              <td>1 minutes ago</td>
            </tr>
            <tr>
              <th scope="row">Great Movie title</th>
              <td>Movie Test</td>
              <td>youji</td>
              <td>1 minutes ago</td>
            </tr>
            <tr>
              <th scope="row">Great Movie title</th>
              <td>Movie Test</td>
              <td>youji</td>
              <td>1 minutes ago</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>


      <div>
        <article class="col-12">
          <div class="d-block d-lg-none">
            <hr class="m-3">
            <ul class="list-group list-group-flush">
              <li class="list-group-item">Best Movie Ever<br>Movie Title<br>1 minutes ago</li>
              <li class="list-group-item">Best Movie Ever<br>Movie Title<br>1 minutes ago</li>
              <li class="list-group-item">Best Movie Ever<br>Movie Title<br>1 minutes ago</li>
              <li class="list-group-item">Best Movie Ever<br>Movie Title<br>1 minutes ago</li>
            </ul>
          </div>
        </article>
      </div>
    </section>

    <nav aria-label="Page navigation example">
      <ul class="pagination d-flex justify-content-center my-5">
        <li class="page-item"><a class="page-link" href="#">Previous</a></li>
        <li class="page-item"><a class="page-link" href="#">1</a></li>
        <li class="page-item"><a class="page-link" href="#">2</a></li>
        <li class="page-item"><a class="page-link" href="#">3</a></li>
        <li class="page-item"><a class="page-link" href="#">Next</a></li>
      </ul>
    </nav>
  </div>
```





### 이 문제에서 어려웠던 점

article과 table의 grid를 구성할 때, d-block과 d-lg-none을 사용해야 한다는 것을 알아내는 데에도 오래 걸렸으나, 실제로 이 코드가 어떻게 작동하며, 어디에 선언해야 하는지 알아내는 데에 오래 걸렸다. div 와 class를 어디에 어떻게 써야 코드가 정확하게 원하는 대로 작동하는지 공부할 필요가 있다고 느꼈다.



### 내가 생각하는 이 문제의 포인트

grid를 table과 article과 같은 큰 요소에게 적용하며, d-block과 d-none을 사용하는 법 익히기.

