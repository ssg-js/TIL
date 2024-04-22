- Flexbox는 모던 웹을 구현하기 위해 기존 layout보다 더 세련된 방식의 니즈에 나온 CSS3의 새로운 layout 방식, 정렬에 강점이 있음

- 사용방법
  
  - 스타일에 display: flex 추가
  - 부모요소가 inline 요소인 경우 flex 대신 inline-flex 추가

- 장점
  
  1. 한줄의 코드로 수평정렬이 가능

- flexbox 구성
  
  - main axis(주축)에 맞춰 flex-item들이 정렬되고, cross axis를 수직 축이라고 한다.
  
  ![Untitled (4).png](C:\Users\likem\AppData\Roaming\marktext\images\283bd263cab45c149afc9cda67e2c896888950db.png)

- **flex container** 속성
  
  - **flex-direction** : 주축의 방향을 설정
    
    1. row : 좌에서 우로 수평 배치
    2. row-reverse : 우에서 좌로 수평 배치(row 반대)
    3. column : 위에서 아래로 수직 배치
    4. column-reverse : 아래에서 위로 수직 배치(column 반대)
  
  - **flex-wrap** : flex-item들이 flex container의 크기를 넘어갈 경우**(width 기준)** 개행할건지를 정하는 속성이다.
    
    - nowrap : 개행하지 않고 1열에 모두 배치한다. **기본값**이고 각 flex-item의 크기는 1열에 다 들어갈 수 있는 크기로 최대한 줄어든다.
    - wrap : flex-item들의 width가 flex container의 width를 넘는 경우 개행한다. 기본적으로 위에서 아래, 좌에서 우로 개행한다.
    - wrap-reverse : 아래에서 위, 우에서 좌로 개행한다.
  
  - **flex-flow :** flex-direction 과 flex-wrap을 동시에 설정가능. 기본값은 row nowrap
    
    ![Untitled (5).png](C:\Users\likem\AppData\Roaming\marktext\images\4d17f387df511b7df75f5355de9323ebdc05a3a9.png)
  
  - **justify-content** : 주축 방향으로 아이템들의 정렬 방법을 결정
  
  - **align-items** : 주축의 수직방향으로 아이템들의 정렬 방법을 결정. flex item들에 모두 영향을 줌
  
  - align-content : 주축의 수직방향으로 아이템들을 정렬함

  align-items와 align-content의 차이 [(참조)](https://letsgojieun.tistory.com/49)

- **flex item** 속성
  
  - order : item의 정렬 순서를 정한다. 기본배치는 container에 추가된 순서이고 기본값은 0이다.
  
  - flex-grow : 너비에 대한 확대인자를 가진다. 기본값은 0이다.
    
    다른 요소를 1, 해당 요소를 3 주면 너비를 3배 더 차지하게 된다.
    
    ![Untitled (6).png](C:\Users\likem\AppData\Roaming\marktext\images\0df9d465313c0a27e23c0b711d8727b4621a4d92.png)
  
  - flex-shrink : 너비에 대한 축소인자를 가진다. 기본값은 1이며, 0일 시 축소가 풀린다.
  
  - flex-basis : 너비 기본값을 px, % 등의 단위로 지정한다. 기본값은 auto.
  
  - flex : flex-grow, flex-shrink, flex-basis 속성을 다 지정할 수 있다. 기본값은 0 1 auto.
    
    ![Untitled (7).png](C:\Users\likem\AppData\Roaming\marktext\images\26bc8d6bb4b4ff200dcd18a73accd4872721154c.png)
  
  - align-self : flex container의 align-items 속성보다 우선하여 개별 item을 정렬한다. 기본값은 auto

- float의 동작에 대해 설명해주세요. [(참조)](https://poiemaweb.com/css3-float)
  
  - flexbox 레이아웃 사용시 더 간편하지만 지원하지 않는 IE를 고려해서 사용함
  - 사용
    - none : 요소를 띄우지 않는다 (기본값)
    - right : 요소를 오른쪽으로 이동한다
    - left : 요소를 왼쪽으로 이동한다.
  - 정렬
    - 먼저 선언된 요소가 먼저 띄워진다.
  - 관련 문제
    - **float 프로퍼티가 선언된 요소와 float 프로퍼티가 선언되지 않은 요소간 margin이 사라지는 문제**
      - float 이 선언된 요소는 떠있는 상태이기 때문에 요소가 margin이 적용되지 않음
      - 해결책 : float 이 선언되지 않은 요소에 overflow : hidden 을 추가
        - `overflow: hidden` 프로퍼티는 자식 요소가 부모 요소의 영역보다 클 경우 넘치는 부분을 안보이게 해주는 역할을 하는데 여기서는 float 프로퍼티가 없어서 제대로 표현되지 못하는 요소를 제대로 출력해줌
    - **float 프로퍼티가 선언된 자식 요소를 포함하는 부모 요소의 높이가 정상적으로 반영되지 않는 문제**
      - float 이 선언된 요소는 떠있기 때문에 부모 요소의 높이에 영향을 주지 않음
      - 해결책 : float 이 선언된 요소에 overflow : hidden 추가





참조) [CSS3 Flexbox Layout | PoiemaWeb](https://poiemaweb.com/css3-flexbox)


