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

- **View - Controller** : View에서 **UserAction**을 Controller에 전달하면 Controller가 View를 **Update**

- **Controller - Mode**l : Controller가 Model을 **Update**하면 Model은 관련 정보를 Controller에 **Notify**


