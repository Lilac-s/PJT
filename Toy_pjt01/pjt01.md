# PJT 01

### 이번 PJT 를 통해 배운 내용

- dictionary 사용법
- for 문 사용법과 들여쓰기의 중요성
- 다른 사람의 코드 설명을 듣는 일이 효율적이라는 것을 알게 되었다.
- 코드 재사용을 위해 다음 단계에서 사용하기 편한 방식으로 코드를 짜야 한다는 것을 느꼈다.



### A. 제공되는 영화 데이터의 주요내용 수집

샘플 영화데이터가 주어집니다. 이중 서비스 구성에 필요한 정보만 뽑아 반환하는 함수를 완성합니다. 완성된 함수는 다음 문제의 기본기능으로 사용됩니다.

- 요구사항

  - 데이터
    - 제공되는  movie.json 파일을 활용합니다.
    - movie.json은 ‘쇼생크 탈출’ 영화 정보를 가지고 있습니다.
    - 샘플 영화데이터에서 서비스 구성에 필요한 정보만 뽑아 반환하는 함수를 완성합니다.
  - 결과
    - 제공된 데이터에서 id, title, poster_path, vote_average, overview, genre_ids 키에 해당하는 정보만 가져옵니다.
    - 가져온 정보를 새로운 dictionary로 반환하는 함수 movie_info를 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  def movie_info(movie):
      # 자료 추출
      id = movie['id']
      title = movie['title']
      poster_path = movie['poster_path']
      vote_average = movie['vote_average']
      overview = movie['overview']
      genre_ids = movie['genre_ids']
      # dictionary 생성
      movie_info_dict = {'id' : id, 'title' : title, 'poster_path' : poster_path, 'vote_average' : vote_average, 'overview' : overview, 'genre_ids' : genre_ids}
      return movie_info_dict
  ```

  주어진 데이터에서 하나하나 자료를 딕셔너리 추출로 꺼내고,

  다시 dictionary를 생성했습니다.

  

  - **이 문제에서 어려웠던 점**

  문제를 처음 열었을 때, movie.json을 불러와야 하는지부터 고민했습니다.

  원래 있던 코드를 차근차근 읽고, 팀원의 도움을 받아 기본 코드가 어떤 역할을 하는지 이해했습니다.

  - 내가 생각하는 이 문제의 포인트
  
  딕셔너리를 사용하는 법을 알고 직접 사용하는 것이 포인트라고 생각합니다.



### 후기

원래 있던 코드가 어떤 역할인지 알고 난 이후부터는 어렵지 않았습니다. 다만 코드가 좀 복잡해 보여서 그것을 고치고 싶다는 생각이 들었습니다. 

problem_c 까지 풀고 나니, a에서부터 for문을 사용하여 코드를 짰다면 c에서 problem을 해결할 때 좀 더 수월하게 해결할 수 있었을 거라는 생각이 들었습니다. 코드의 재사용성을 정확히 어떻게 높일 수 있을지는 아직 모르지만, 그 중요성을 간접적으로 느낄 수 있었습니다.



### B. 제공되는 영화 데이터의 주요내용 수정

이전단계에서 만들었던 데이터 중 genre_ids를 genre_names로 바꿔 반환하는 함수를 완 성합니다. 완성된 함수는 다음 문제의 기본기능으로 사용됩니다. 

- 요구사항

  - 데이터
    - 제공되는 movie.json, genres.json 파일을 활용합니
    - movie.json은 ‘쇼생크 탈출’ 영화 정보를 가지고 있습니다.
    - genres.json은 장르의 id, name 정보를 가지고 있습니다.
  - 결과
    - 제공된 데이터에서 id, title, poster_path, vote_average, overview, genre_ids 키에 해당하는 정보만 가져옵니다.
    - genres.json파일을 이용하여 genre_ids를 genre_names로 변환하여 dictionary 에 추가합니다.
    - 완성된 dictionary를 반환하는 함수 movie_info를 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  def movie_info(movie, genres):
      
      #movie 안에 있는 id 추출
      genre_ids = movie['genre_ids']
      genre_names = [] #장르 이름을 받을 변수와 리스트 생성
  
      for i in genres: #장르들 안을 반복하는 i 생성
          if i['id'] in genre_ids: #id를 대치시켜서 같은 id라면,
              genre_names.append(i['name']) #장르 이름을 받는 변수 genre_names에 추가
      
      # 자료 추출
      id = movie['id']
      title = movie['title']
      poster_path = movie['poster_path']
      vote_average = movie['vote_average']
      overview = movie['overview']
      # dictionary 생성
      movie_info_dict = {'genre_names' : genre_names, 'id' : id, 'title' : title, 'poster_path' : poster_path, 'vote_average' : vote_average, 'overview' : overview}
      return movie_info_dict
  
  ```

  

  - **이 문제에서 어려웠던 점**

  처음에 문제 자체의 의도를 이해하지 못해 헤매다가, 주어진 조건을 print 해보고 차근차근 이해했습니다.  append 함수를 사용해야 한다는 것도 팀원의 도움을 받아 알게 되었고, append 함수를 사용하려면 그것을 받을 수 있는 리스트를 생성해야 한다는 것을 알아내기까지 시간이 걸렸습니다.

  - 내가 생각하는 이 문제의 포인트

  주어진 데이터 값을 대치하고, 변환하여 추가하는 함수 구현하는 법 익히기.

### 후기

문제 자체를 이해하는 데 꽤 오랜 시간을 썼습니다. genre_ids를 genre_names로 변환하라는 것이 어떤 뜻인지, 데이터를 직접 눈으로 몇 번이고 확인하기 전까지는 이해하지 못했습니다. 자료를 확인하고 문제를 이해한 후에는 append 함수를 사용해야 한다는 것을 알아차리기까지 오랜 시간이 걸렸습니다. 문제의 의도를 파악하는 것이 얼마나 중요하고, 생각보다 어려운 일인지 느낄 수 있었습니다.



### C. 다중 데이터 분석 및 수정

TMDB기준 평점이 높은 20개의 영화데이터가 주어집니다. 이 중 서비스 구성에 필요한 정 보만 뽑아 반환하는 함수를 완성합니다. 완성된 함수는 향후 커뮤니티 서비스에서 제공되는 영화 목록을 제공하기 위한 기능으로 사용됩니다 

- 요구사항

  - 데이터
    - 제공되는 movie.json, genres.json 파일을 활용합니다.
    - movies.json은 영화 전체 정보를 가지고 있습니다.
    - genres.json은 장르의 id, name 정보를 가지고 있습니다.
  - 결과
    - 이전 단계의 함수 구조를 재사용합니다.
    - 영화 전체 정보를 수정하여 반환하는 함수 movie_info를 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  def movie_info(movies, genres):
      
      info_movies = list() #영화 정보를 받아 올 리스트 선언
  
      for movie in movies: #movies 안의 정보를 차례대로 가져올 변수 movie 생성
          
          genre_ids = movie['genre_ids'] #여기는 B번과 동일합니다.
          genre_names = []
  
          for i in genres:
              if i['id'] in genre_ids:
                  genre_names.append(i['name'])
          
              id = movie['id']
              title = movie['title']
              poster_path = movie['poster_path']
              vote_average = movie['vote_average']
              overview = movie['overview']
          
              movie_info_dict = {'genre_names' : genre_names, 'id' : id, 'title' : title, 'poster_path' : poster_path, 'vote_average' : vote_average, 'overview' : overview}
      
          info_movies.append(movie_info_dict) #생성된 dictionary를 info_movie에 추가
  
      return info_movies
  
  ```

  

  - **이 문제에서 어려웠던 점**

  문제 의도를 파악하는 시간은 b보다 짧아졌습니다. 그래서 코드를 적는 것은 시간이 적게 들었으나, 계속해서 한 종류의 값만 출력되었습니다. 팀원의 도움으로 해결하였으나 for 문 들여쓰기의 원리를 이해하는 데에 어려움을 겪었습니다.

  

  - 내가 생각하는 이 문제의 포인트

  들여쓰기 이해하기

### 후기

이전보다 코드가 잘 적혀서 조금 자신감이 붙었다가, 다시 혼란에 빠졌다. 들여쓰기의 문제라는 것을 구글링으로 찾아냈을 때 이것저것 들여쓰고, 다시 내어쓰고 반복해 보았는데 원리 자체를 완벽히 알지 못하니 해결이 될 리가 없었다. 팀원의 도움을 받아 해결했고, 왜 이게 이렇게 되었는지는 이해했지만 다른 문제에서 비슷한 어려움을 겪을 때 그걸 잘 해결하려면 기초를 더 공부하고 코드를 더 열심히 고민해보아야 할 것 같다.



### D. 알고리즘을 통한 데이터 출력

세부적인 영화 정보 중 수익 정보(revenue)를 이용하여 모든 영화 중 가장 높은 수익을 낸 영화를 출력하는 알고리즘을 작성합니다. 해당 데이터는 향후 커뮤니티 서비스에서 메인 페 이지 기본정보로 사용됩니다. 

- 요구사항

  - 데이터
    - movies.json과 movies폴더 내부의 파일들을 사용합니다.
    - movies.json은 영화 전체 정보를 가지고 있습니다.
    - movies 폴더 내부의 파일들은 각 영화의 상세정보를 가지고 있습니다.
    - movies 폴더의 파일의 이름은 영화의 id로 구성되어 있습니다. 아래는 13번 id를 가지고 있는 영화의 상세정보입니다.
    - 수익정보는 상세정보 파일을 통해 확인할 수 있습니다. 힌트 : 반복문을 통해 상세 정보 파일을 오픈해야 합니다.
  - 결과
    - 수익이 가장 높은 영화의 제목을 출력하는 함수 max_revenue를 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  def max_revenue(movies):
  
      max_value = 0 # 최다 수익을 표현하는 변수
      max_title = '' # 최다 수익을 창출한 영화를 표현하는 변수
  
      for movie in movies:#movies 안을 순회하며 최다 수익을 찾는 변수 movie
          _id = movie.get('id') # id를 가지고 오기
          # id로 상세정보 파일을 열기
          movie_detail = open(f'data/movies/{str(_id)}.json', encoding='UTF8')
          movie_detail_list = json.load(movie_detail)
  
          # 최다 수익 영화를 찾아 제목 할당
          if max_value < movie_detail_list['revenue']:
              max_value = movie_detail_list['revenue']
              max_title = movie_detail_list['title']
          
      return max_title
  
  ```

  

  - **이 문제에서 어려웠던 점**

  문제에서 이야기하는 '알고리즘'을 통한 데이터 출력이 무엇인지 이해하는 데에 한참 걸렸다. open을 사용하는 걸 생각해 내기 어려웠다. 

  

  - 내가 생각하는 이 문제의 포인트

  상세정보 파일을 가져와서 사용하기

### 후기

문제에서 제공하는 데이터를 가져와서 open으로 사용해 보았다. 앞서서 마주한 A, B, C 문제에서 계속된 어려움이 어디에서 왔는지 제대로 파악하지 못했는데, 이 문제에서 알 수 있었다. 눈에 보이지 않는, 어떤 모양인지 모르는 데이터들이 있으니 문제가 요구하는 바를 이해하기가 더 어려웠던 것이었다. 하지만 예전에 화학을 공부했던 때 처럼, 눈에 보이지 않아도 그것을 파악하는 일에 익숙해질 것이다. 또한 데이터는 열면 보이니 사실 눈에 보이지 않는 것이 아니다. 불러 와서 보이게 만드는 게 어려울 뿐이다. 이 문제를 마지막으로 다음 E 문제를 풀기 위해 주말 동안에는 기초를 다질 생각이다. 또한 앞으로 컴퓨터라는 것에 좀더 익숙해지도록 CS공부를 적극적으로 해야 하겠다고 느꼈다.

