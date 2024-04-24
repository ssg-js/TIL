# Docker 란

#### Docker란

- 어플리케이션을 패키징 할 수 있는 툴

- **컨테이너**라는 소프트웨어 유닛 안에 **어플리케이션**과 구동하기 위한 **시스템 툴**, **환경설정**과 **dependencies**를 하나로 묶어서 **다른 OS, PC에서 안정적으로 구동**할 수 있게 하는 툴 => 그렇다면 vm과 같지 않나??라는 물음이 생김

#### VM vs Docker

- **VM** : Infrastructure 위에 Hypervisor 소프트웨어(vmware, VirtualBox)에서 각각의 가상머신을 만듬 => 각 가상 머신은 OS를 포함해 굉장히 무거움(리소르를 많이 잡아먹음)

- **Conatainer** : Infrastructure 하드웨어에 설치된 운영체제, Host OS에서 Container Engine 소프트웨어를 설치에 각 컨테이너 별로 독립된 환경에 어플리케이션을 구동하게 해줌 => OS를 포함하지 않고 Container Engine에 설치된 Host OS를 공유(공부하기: 운영체제와 커널)
  
  - Container Engine 중에 가장 많이 쓰이는 게 **Docker**

#### Building Container 요소 3가지

- Dockerfile
  
  - 컨테이너 생성 설명서
  
  - copy files, dependencies, 환경변수, setup scripts

- Image
  
  - 모든 세팅들이 포함 => 실행되고 있는 어플리케이션 상태를 저장
  
  - 변경이 불가능함

- Container
  
  - Image를 이용해 고립된 파일 시스템 안에서 구동함

#### Container 배포

1. Local Machine에서 Docker Image 생성

2. Github 같은 Container Resistry에 Image를 push

3. 서버에서 Image를 들고와 Docker로 컨테이너에서 어플리케이션 실행

### Container Resistry

- public
  
  - **dockerhub**, REDHAT, GitHub Packages

- private : 회사에서 Docker Image를 보호하기 위해 사용
  
  - AWS, Google Cloud, Azure
