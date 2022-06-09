# PJT 02

### 이번 pjt를 통해 배운 내용

- import requests
- request를 이용해서 요청 보내기
- API 활용하기



### A. 인기 영화 조회

- 요구사항

  - 요청
    - requests를 이용하여 인기 영화 정보(Get Popular)에 요청을 보냅니다.
  - 결과
    - popular를 기준으로 받아온 데이터에서 영화 리스트의 개수를 계산합니다.
    - 계산한 정보를 반환하는 함수 popular_count를 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  import requests
  
  
  def popular_count():
      URL = 'https://api.themoviedb.org/3/movie/popular' #URL 불러오기
      # param 지정하기
      param = {
          'api_key' : '39ee726a513e344feec7d0b9c041b3ca', 
          'language' : 'ko'
      }
  
      response = requests.get(URL, params = param) #requests로 요청 보내기
      movie_dict = response.json() #json파일로 딕셔너리 만들기
      return len(movie_dict['results']) #결과 추출
      
  
  if __name__ == '__main__':
      """
      popular 영화목록의 개수 출력.
      """
      print(popular_count())
      # => 20
  
  ```

  

  

  - **이 문제에서 어려웠던 점**

  param 지정하고, URL 설정하기



### 후기

처음에 어디서부터 어떻게 건드려야 할지 감이 잡히지 않아서 팀원의 도움을 받았다. param에 대한 정의를 아직도 잘 모르겠다. 프로젝트를 끝내고 나서 좀더 공부할 계획이다. json파일로 딕셔너리를 만들었는데, 대부분의 코드들이 정확히 어떤 과정을 거쳐서 이렇게 만들어지는지 완벽하게 이해하지 못했다.



### B. 특정 조건에 맞는 인기 영화 조회 1

- 요구사항

  - 요청
    - requests를 이용하여 인기 영화 정보(Get Popular)에 요청을 보냅니다.
  - 결과
    -  받아온 데이터에서 vote_average를 기준으로 점수가 8 이상인 영화들의 목록을 리스트로 반환하는 함수 vote_average_movies를 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  import requests
  from pprint import pprint
  
  
  def vote_average_movies():
      URL = 'https://api.themoviedb.org/3/movie/popular'
      param = {
          'api_key' : '39ee726a513e344feec7d0b9c041b3ca', 
          'language' : 'ko'
      }
  
      response = requests.get(URL, params = param)
      movie_dict = response.json()
  
      movie_average = [] #리스트를 받을 변수 선언
      for i in range(len(movie_dict['results'])): # result 길이만큼 순회하는 i 설정
          if int(movie_dict['results'][i]['vote_average']) >= 8:# 8보다 큰 값 추출
              movie_average.append(movie_dict['results'][i]) # 리스트에 append
      return movie_average
  
  
  
  if __name__ == '__main__':
      """
      popular 영화목록중 vote_average가 8 이상인 영화목록 출력.
      """
      pprint(vote_average_movies())
      # => 영화정보 순서대로 출력
  ```

  

  - **이 문제에서 어려웠던 점**

  리스트 인덱싱할때 조금 까다로웠습니다.

  

### 후기

A번에서 완성한 코드를 그대로 사용하니 B번은 어렵지 않았다. 늘 하던 대로 리스트 인덱싱을 하고, 그중에 조건에 맞는 값을 추출해서 append하고 리턴하였다. 다만, 이것보다 간략하고 보기 쉬운 코드가 분명히 있을 텐데 그걸 쓰지 못한 게 아쉽다. 아직은 코딩 자체가 손에 덜 익은 것 같다는 생각을 많이 하게 됐다. i를 굳이 range 안을 돌리지 않고 그냥 값 안을 돌려서 추출할 수도 있었을 텐데.. 



### C. 특정 조건에 맞는 인기 영화 조회 2

- 요구사항

  - 요청
    - requests를 이용하여 인기 영화 정보(Get Popular)에 요청을 보냅니다.
  - 결과
    - 받아온 데이터 중 평점이 높은 영화 다섯개의 정보를 리스트로 반환하는 함수 ranking을 완성합니다.

- 결과

  - 문제 접근 방법 및 코드 설명

  ```python
  import requests
  from pprint import pprint
  
  
  def ranking():
      URL = 'https://api.themoviedb.org/3/movie/popular'
      param = {
          'api_key' : '39ee726a513e344feec7d0b9c041b3ca', 
          'language' : 'ko'
      }
  
      response = requests.get(URL, params = param)
      movie_dict = response.json() 
      results = movie_dict.get('results') # results 값만 꺼내서 할당
  
      def func(dic): 
          return dic.get('vote_average') #vote_average를 추출하는 함수 설정
  
      results.sort(key=func, reverse=True) # results를 정렬, reverse
      results = results[:5] # 슬라이스로 높은 5개의 영화 추출
      for i in results:
          i.get('vote_average') # vote_average 값 기준으로 정렬하기 위한 for문
  
      return results
  
  
  if __name__ == '__main__':
      """
      popular 영화목록을 정렬하여 평점순으로 5개 영화.
      """
      pprint(ranking())
      # => 영화정보 순서대로 출력
  
  ```

  

  - **이 문제에서 어려웠던 점**

  .sort()를 써야 한다고 생각했지만 구현하는 방법을 떠올리기가 쉽지 않았습니다.

  


### 후기

처음에는 B번과 똑같이 append하는 방식에 슬라이스를 추가하였다. 그리고 그 사이에 정렬을 하려고 했는데 어떻게 정렬을 해야 할지, 정렬을 하는 대상은 어떻게 추출해야 할지가 막막했다. 설명을 들으며 하나하나 해나가니 이해가 되었지만 스스로 처음부터 끝까지 다시 풀어보는 과정이 필요하다고 느꼈다.





