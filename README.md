# melon-bigdata-project

**2019 2학기 빅데이터분석 과제 : 미니프로젝트**

### subject

melon 이용자들이 음악을 활발하게 듣는 시기는? 

- 점유율 1위인 음원사이트 melon에서 2010년부터 2019년까지의 모든 주간차트 순위 변동 추이를 분석

  - 순위 변동 추이를 보고 가장 순위 변동 폭이 큰 구간 찾기
  
- 선형 회귀분석을 통해 미래의 순위변동 추이 예측해보기

### data crawling

beautifulSoup4를 이용해 파싱하고, selenium으로 멜론 차트파인더를 통해 원하는 데이터 추출 자동화

![image](https://user-images.githubusercontent.com/61912635/106713711-3057d480-663e-11eb-9a1b-54faf184ffe6.png)
2010년부터 2019년 11월까지 매주 주간 top100을 차트파인더에서 확인할 수 있고, 웹 크롤링으로 데이터를 수집

![image](https://user-images.githubusercontent.com/61912635/106713731-351c8880-663e-11eb-85c0-8d604ba9b2ad.png)

데이터는 [연도//월//주//순위//제목//가수//변동순위//순위 변동상태(상승or하락)] 형식으로 저장

각각 요소를 //로 구분한 이유는 ,를 사용하면 split했을 때 제목에 ,가 있는 것까지 포함해서 split되기 때문

데이터 예시

![image](https://user-images.githubusercontent.com/61912635/106714769-a446ac80-663f-11eb-9462-12c23e522c40.png)

### data analysis

크롤링한 데이터에서 변동 순위와 상태를 보고 순위 변동 추이 (+,-)로 판단하여 열 추가

![image](https://user-images.githubusercontent.com/61912635/106714812-b0326e80-663f-11eb-9255-629e6cd20cc6.png)

월간 순위 변동이 가장 큰 달은 10월

순위 변동이 크다 = 이용자들이 새로운 노래를 많이 찾아 듣는다 라는 가정하에 지난 10년간 10월달에 발매한 음원이 가장 좋은 음원성적을 냈다고 볼 수 있음

![image](https://user-images.githubusercontent.com/61912635/106715300-3e0e5980-6640-11eb-9b56-fcc66e32a233.png)

### linear regression

월 별 순위변동 추이 그래프를 보고 미래의 순위 변동을 예측할 수 있을지 간단한 선형회귀분석으로 예측해봄

1월부터 12월까지 아래와 같은 그래프에서 선형 모델로 회귀했을 때 5월 데이터가 가장 오차가 작았음 (0.91)

![image](https://user-images.githubusercontent.com/61912635/106715957-24214680-6641-11eb-8371-8404b8961711.png)

간단한 선형모델에서 연도를 입력하면 5월의 예측 순위 변동 수치를 알려줌

