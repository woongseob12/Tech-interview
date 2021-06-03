# Project 정리

## 클라우드

### 클라우드란?

`물리적인 서버 없이 인터넷에 접속하여 다양한 자원을 사용할 수 있게 하는 컴퓨터 리소스 이용형태`

**물리서버와 클라우드 서버의 특징?**

- 소유자와 사용자가 다르다
- 물리서버의 경우 일반적으로 기업이 서버를 소유
- 반면 AWS는 Amazon이 모든 리소스를 소유하고, 해당 리소스를 서비스로 만든 것을 사용하는 형태

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
  - 사용한 만큼 지불(PAYG, Pay-as-you-go)
  - 높은 수준의 탄력성
- Private Cloud:
  - 한 조직만을 위하여 운영되는 클라우드
  - 보안 및 신뢰성 제고

### OpenStack이란?

![image](https://user-images.githubusercontent.com/55429912/120616946-9e999000-c494-11eb-8fcd-89041c5942fe.png)

`풀링된 가상 리소스를 사용하여 Private, Public 클라우드를 구축하고 관리하는 오픈소스 플랫폼`

---

### VPNaaS란?

1. VPN이란?

- 사설 네트워크나 공용 네트워크의 지점간 연결을 말하며 클라이언트는 터널링 프로토콜이라는 TCP/IP 기반 프로토콜을 사용하여 VPN서버의 가상 포트를 통해 호출합니다.
- 데이터는 캡슐화 암호화 되어 암호화키가 없으면 해독할 수 없습니다.
- 특정 네트워크의 데이터 송수신에 보안 및 방화벽 기능이 중요한 부분을 차지할 때 사용됩니다.

2. VPNaaS란?

- 동적, 정적 라우팅을 지원하여 멀티 터널링, 보안 프로토콜의 다양함을 목적으로 하여 하바나 버전에서 릴리즈 되었습니다.
- IPsec을 기반으로한 VPN을 오픈 소스 기반으로 구현 제공합니다.

3. Neutron이란?

![image](https://user-images.githubusercontent.com/55429912/120623806-05ba4300-c49b-11eb-8490-66567235a03b.png)

`OpenStack에서 생성되는 인스턴스들의 네트워크 서비스를 생성/ 관리에 대한 프로젝트로, 사용자는 Neutron API를 이용해 Neutron Plug-in을 통해서 네트워크를 구성할 수 있다.`

4. Openstack Neutron에서의 VPN 통신

   ![image](https://user-images.githubusercontent.com/55429912/120620525-03a2b500-c498-11eb-8179-980993cbf7b5.png)

   VPNaaS 설정 FLOW

   1. IKE Policy 생성
   2. IPSec Policy 생성
   3. VPN Service 생성
   4. IPSec Site Connection 생성

---

- nginx
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
