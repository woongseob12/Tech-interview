# Project 정리

## 클라우드

### 클라우드란?

`물리적인 서버 없이 인터넷에 접속하여 다양한 자원을 사용할 수 있게 하는 컴퓨터 리소스 이용 형태`

**물리서버(On-Premises)와 클라우드 서버의 특징?**

- 소유자와 사용자가 다르다
- 물리서버의 경우 일반적으로 기업이 서버를 소유하여 사용
- AWS와 같은 클라우드 서버는 Amazon이 모든 리소스를 소유하고, 해당 리소스를 서비스로 만든 것을 사용자가 사용하는 형태

**렌탈 서버의 3가지 형태?**

1. 공용서버: 1대의 물리서버를 분할 한 형태
   - 다른 사용자의 영향을 받을 수 있음
2. 전용서버: 1대의 물리서버를 점유하는 형태
   - 다른 사용자의 영향을 받진 않으나 비쌈
3. 가상전용서버: 1대의 물리서버 위에 있는 가상서버를 점유

**Public Cloud와 Private Cloud의 차이**

**누구에게 서비스를 제공하는가**

- Public Cloud:
  - 다수의 대중을 위하여 인터넷 기반으로 운영되는 클라우드
  - 사용한 만큼 지불(PAYG, Pay-As-You-Go)
  - 높은 수준의 탄력성
- Private Cloud:
  - 한 조직만을 위하여 운영되는 클라우드
  - 보안 및 신뢰성 제고

### Virtualization(가상화)

`컴퓨터에서 CPU, 메모리, I/O등의 물리적인 리소스를 추상화하는, 즉 물리적인 자원을 논리적인 자원으로 보이게하는 기술`

### Hypervisor(하이퍼바이저)

![image](https://user-images.githubusercontent.com/55429912/120633203-d577a200-c4a4-11eb-8d47-ca2255a92d14.png)

`호스트 컴퓨터에서 다수의 OS를 동시에 실행하기 위해 하드웨어 자원을 논리적인 플랫폼(platform)으로 가상화해주는 소프트웨어`

- 논리적인 자원으로 가상화된 환경 위에 여러 OS를 동시에 운영할 수 있다.

**Hypervisors 분류**

1. 설치 방식에 따른 분류

   - Type 1(Native or Bare metal)

     ![image](https://user-images.githubusercontent.com/55429912/120633483-2ab3b380-c4a5-11eb-97c6-eca0106b672c.png)

     - 호스트의 하드웨어 상에서 바로 동작하며, 게스트 OS를 관리
     - CPU 가상화를 지원해야 함
     - KVM

   - Type 2(Hosted)

     ![image](https://user-images.githubusercontent.com/55429912/120633611-4d45cc80-c4a5-11eb-9822-0c6248998a81.png)

     - 호스트의 OS상에서 Hypervisor 동작
     - Hypervisor는 OS를 통해 H/W를 호출
     - VirtualBox, QEMU

2. 가상화에 따른 분류

   - Full Virtualization(전가상화)

     - 하드웨어 전체를 가상화(Guest OS를 변경없이 사용 가능)
     - CPU의 지원이 필요
     - KVM

   - Para Virtualization(반가상화)
     - 하드웨어를 완전히 가상화하지 않음
     - Guest OS의 직접 하드웨어 제어가 안되고 하이퍼바이저를 통해 제어
     - QEMU

**KVM**: Linux 기반에서 CPU 기반의 전가상화, 즉 하드웨어 전체를 가상화 하는 것을 지원하는 하이퍼바이저
**QEMU**: 호스트머신과 독립적으로 가상화된 하드웨어 및 아키텍처를 동작 시킬수 있는 에뮬레이션이 가능한 하이퍼바이저
**Libvirt**: 가상화를 관리하기 위한 오픈 소스 API

---

### Cloud 서비스의 종류

![image](https://user-images.githubusercontent.com/55429912/120635353-5899f780-c4a7-11eb-9f1d-d3e5c53f555c.png)

1. IaaS(Infrastructure as a Service)

   - 기존에 물리적인 형태로 사용해왔던 스토리지, 서버 등의 인프라를 가상화하여 제공하는 서비스
   - AWS 서비스 중 EC2, S3

2. PaaS(Platform as a Service)

   - 사용자가 원하는 서비스를 개발할 수 있는 OS, 미들웨어 등의 환경(Platform)을 제공하는 서비스
   - 구글의 앱 엔진

3. SaaS(Software as a Service)

   - 클라우드 기반의 응용프로그램을 서비스 형태로 제공하는 것
   - 웹기반 개인용 스토리지 서비스(N드라이브, 구글드라이브 등..)

### OpenStack이란?

![image](https://user-images.githubusercontent.com/55429912/120616946-9e999000-c494-11eb-8fcd-89041c5942fe.png)

`풀링된 가상 리소스를 사용하여 Private, Public 클라우드를 구축하고 관리하는 오픈소스 플랫폼`

- Iaas 형태의 클라우트 컴퓨팅 오픈 소스 프로젝트

**구성 요소**

![image](https://user-images.githubusercontent.com/55429912/120641906-2db3a180-c4af-11eb-8525-dc9257e4c5d6.png)

1. 컴퓨트(Nova)

`Hypervisor를 관리하는 API 제공`

- Instance(VM) 생성 관리

2. 이미지(Glance)

`Openstack에서 운영체제 이미지를 관리`

- VM에 설치된 OS 보관 및 관리

3. 네트워킹(Neutron)

`네트워크와 IP 주소들을 관리하기 위한 시스템`

- 다양한 네트워크 플러그인과 네트워크 모델을 지원

4. 오브젝트 스토리지(Swift)

`대용량, 비정형 데이터를 저장하기에 적합한 스토리지`

5. 아이덴티티(Keystone)

`자원들에 대한 인증관리`

- 로그인을 포함한 여러 형태의 인증을 지원

6. 블록 스토리지(Cinder)

`가상 머신에 영구 스토리지를 추가`

- 볼륨 관리를 위한 인프라를 제공

7. 대시보드 서비스(Horizon)

`오픈스택 대시보드 서비스`

- 사용자가 웹 UI를 통하여 인스턴스 생성, 삭제 및 관리 등을 쉽고 빠르게 처리할 수 있도록 해주는 웹 서비스

**용어 정리**

Instance: 클라우드 상의 가상 서버
Volume: 저장공간
Snapshot: 클라우드 서버나 볼륨을 저장해 백업하는데 사용
Flavor: 인스턴스(가상 서버)의 사양(CPU, 메모리, 하드디스크 사양 등..)

---

### VPNaaS란?

1. VPN(Virtual Private Network)이란?

- 사설 네트워크나 공용 네트워크의 지점간 연결을 말하며 클라이언트는 터널링 프로토콜이라는 TCP/IP 기반 프로토콜을 사용하여 VPN서버의 가상 포트를 통해 호출합니다.
- 데이터는 캡슐화 암호화 되어 암호화키가 없으면 해독할 수 없습니다.
- 특정 네트워크의 데이터 송수신에 보안 및 방화벽 기능이 중요한 부분을 차지할 때 사용됩니다.

2. VPNaaS란?

- 동적, 정적 라우팅을 지원하여 멀티 터널링, 보안 프로토콜의 다양함을 목적으로 하여 하바나 버전에서 릴리즈 되었습니다.
- IPsec을 기반으로한 VPN을 오픈 소스 기반으로 구현 제공합니다.

3. Neutron이란?

![image](https://user-images.githubusercontent.com/55429912/120623806-05ba4300-c49b-11eb-8490-66567235a03b.png)

`OpenStack에서 생성되는 인스턴스들의 네트워크 서비스를 생성/ 관리에 대한 프로젝트로, 사용자는 Neutron API를 이용해 Neutron Plug-in을 통해서 네트워크를 구성할 수 있다.`

---

### 유동(Floating) IP 설정

**Floating IP란?**

![image](https://user-images.githubusercontent.com/55429912/120646808-d9abbb80-c4b4-11eb-9593-025a9a43a987.png)

`오픈스택에서 제공하는 네트워킹 기능 중 하나로, VM이 할당 받은 고정 IP에 공용망에서 할당 받은 IP를 매핑하는 기술`

외부에서 접속할 수 있도록 인스턴스에 Floating IP 설정

1. IP 할당
2. IP를 인스턴스와 연결

---

### Nginx

`경량 웹 서버`

- 클라이언트로부터 요청을 받았을 때 요청에 맞는 정적 파일을 응답해주는 HTTP Web Server로 활용
- Reverse Proxy Server로 활용하여 WAS 서버의 부하를 줄일 수 있는 로드 밸런서로 활용되기도 함

---

### Doker, K8S

---

- 리눅스 셸, 프로세스, 에디터, 운영 및 관리...

---

## 알고리즘

- 알고리즘 파일에 일괄 정리

---

## 캡스톤 디자인

- NodeMCU
- Arduino IDE
- C++
- HTML/ CSS
- GET, POST

---

## 시스템 프로그래밍

- 메모리 계층 구조
- 프로그램 최적화
- 링킹
- Stack Overflow를 이용한 프로그램 해킹

---

## 데이터 통신

- ARP Spoofing
- 네트워크 공격 유형

---

## 컴퓨터 구조

- Datapath 설계
- MIPS 명령어 파이프라인 5단계
- 단일 사이클의 문제점

---

## 영상처리 & 머신러닝

- OpenCV
- Dlib

---

## Back-End

- Spring

---

## Front-End

- Vue
