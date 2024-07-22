# MVC, MVP, MVVM 패턴

## MVC 패턴

- 모델(Model), 뷰(View), 컨트롤러(Controller)로 이루어진 디자인 패턴

- **Model**
  
  - Model은 애플리케이션의 데이터인 데이터베이스, 상수, 변수 등을 뜻함
  
  - View에서 데이터를 수정하거나 생성할 때 Controller를 통해 Model이 업데이트 또는 생성됨

- **View**
  
  - View는 inputbox, checkbox, textarea 등 사용자 인터페이스(UI) 요소를 나타냄
  
  - Model이 가지고 있는 정보를 **따로 저장하지 않아야 하며** 변경이 일어나면 Controller에 전달

- **Controller**
  
  - 하나 이상의 Model과 하나 이상의 View를 잇는 다리 역할
  
  - 이벤트 등 **메인 로직**을 담당함
  
  - Model과 View의 생명주기도 관리함

- **View - Controller** : View에서 **UserAction**을 Controller에 전달함. Controller는 View에게 Model의 데이터를 **Deliver**함

- **Controller - Mode**l : Controller가 Model을 **Update**하면 Model은 관련 정보를 Controller에 **Notify**

- 대표적인 프레임워크 : Spring WEB MVC

#### MVC 패턴 규칙

1. Model은 Controller와 View에 의존하지 않아야함 (Model 내부에 Controller와 View에 관련된 코드가 존재 x)

2. View는 Model에만 의존해야 하고, Controller에 의존하면 안됨

3. View가 Model로부터 데이터를 받을 때는, 사용자마다 다르게 보여줘야 하는 데이터만 받아야함

4. Controller는 Model과 View에 의존해도 됨

5. View가 Model로부터 데이터를 받을 때, 반드시 Controller에서 받아야함

#### MVC 패턴의 장단점

- 장점
  
  - 애플리케이션의 구성 요소를 **세 가지 역할로 구분해** 각 구성 요소에만 집중하는 개발 가능
  
  - 재사용성과 확장성이 용이

- 단점
  
  - 애플리케이션이 복잡해질수록 Model과 View의 관계가 복잡해짐



## MVP 패턴

- Controller가 Presenter로 교체된 패턴

- View와 Presenter가 1:1 관계라 **MVC보다 더 강한 결합**을 지님





[참고자료]

[CS 지식의 정석 | 디자인패턴 네트워크 운영체제 데이터베이스 자료구조 강의 | 큰돌 - 인프런](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A9%B4%EC%A0%91-cs-%ED%8A%B9%EA%B0%95/dashboard)

[[10분 테코톡] 🧀 제리의 MVC 패턴 - YouTube](https://www.youtube.com/watch?v=ogaXW6KPc8I)


