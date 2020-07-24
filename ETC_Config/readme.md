## 추가 설정   

### Grafana의 쿼리 데이터를 숨기는 방법

#### 기본 설명
Grafana는 사용자 권한을 사용하여 사용자가 볼 수 있는 데이터와 행동의 제약을 정의할 수 있다.   
가장 최소 권한인 Viewer는 단순히 Grafana 대시보드를 구경할 수 밖에 없다. 다만 Inspector를 통해 어떤 쿼리가 사용되었는지 볼 수 있는데, Viewer에게 이러한 권한도 허용하고 싶지 않은 관리자도 있을 것 이다.   

Grafana의 설정 파일이나 권한을 자세히 찾아봐도 해당 행동을 제약할 수 있는 설정이 없어서 개발자도구를 사용하여 해당 데이터가 어떤 Javascript파일을 사용하여 보여지는지 알아냈다.

#### 방법
/usr/share/grafana/public/build 디렉토리를 살펴보면 아래 이름과 비슷한 파일을 확인할 수 있다.

````
default~DashboardPage~SoloPanelPage.c8856b8b39626543db12.js
````

해당 파일을 JavaScript Beautifier등을 사용하여 보기 좋게 변환하면 어떤 코드를 지워야 할지 확인할 수 있다.

1. Inspect 항목 숨기기   
Inspect에 Query와 Panel Json 메뉴가 있는데 이를 확인하면 쿼리 내용 조회가 가능하다.   
Inspect의 Query와 Panel Json 메뉴를 숨기려면 아래 코드를 수정한다.
![Alt text](https://raw.githubusercontent.com/chupark/Grafana/master/images2/2.%20hide.png)    

<br>

2. Inspect 블레이드의 Panel Json 정보 숨기기   
사용자가 패널의 데이터 값을 CSV로 추출하길 원할 수 있기 때문에 위에서 진행한 과정에서 Data메뉴만 남겨놓았는데 이를 클릭해서 들어가면 JSON과 Query 메뉴가 보인다. 여전히 데이터 확인이 가능하므로 아래 방법으로 숨긴다.   
![Alt text](https://raw.githubusercontent.com/chupark/Grafana/master/images2/3.%20hide.png)    

<br>

3. Inspect 블레이더의 Query 정보 숨기기   
위와 같은 이유로 Query 정보를 숨긴다. 아래 코드를 삭제하여 데이터가 안보이게 할 수 있다.   
![Alt text](https://raw.githubusercontent.com/chupark/Grafana/master/images2/4.%20hide.png)    

<br>

4. Inspect 블레이드의 JSON, Query 메뉴 숨기기   
JSON과 Query 메뉴를 완전히 지워버리려면 아래 사진의 코드를 찾아서 삭제한다.   
![Alt text](https://raw.githubusercontent.com/chupark/Grafana/master/images2/1.%20hide.png)    