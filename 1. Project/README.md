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

- Iaas 형태의 클라우드 컴퓨팅 오픈 소스 프로젝트

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

`자원들에 대한 인증 관리`

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

- IPsec을 기반으로 Private 네트워크와 public cloud 사용자간의 안전한 연결을 보장

1. Neutron이란?

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

### Docker

`리눅스 컨테이너를 기반으로 하여 특정한 서비스를 패키징하고 배포하는 오픈소스 가상화 플랫폼`

**컨테이너란?**

![image](https://user-images.githubusercontent.com/55429912/120686767-4dad8a00-c4dc-11eb-8d41-327fe1b45d27.png)

`격리된 공간에서 프로세스가 동작하는 기술`

- 애플리케이션 구동에 필요한 라이브러리 및 실행파일만 존재

**이미지(Image)?**

![image](https://user-images.githubusercontent.com/55429912/121000856-a6737000-c7c5-11eb-9efc-1f9d592eedb5.png)

`컨테이너 실행에 필요한 파일과 설정값 등을 포함하고 있는 것`

- 상태값을 가지지 않고 변하지 않음(Immutable)
- 이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 더이상 의존성 파일을 컴파일하고 별도의 설치가 필요 없음
  - 새로운 서버가 추가되면 미리 만들어 놓은 이미지를 다운받고 컨테이너를 생성하면 됨

**레이어 저장방식**

![image](https://user-images.githubusercontent.com/55429912/121001380-31546a80-c7c6-11eb-8337-63567cf30c10.png)

`이미지를 빌드할 때마다 이미 생성된 레이어가 캐시되어 재사용되기 떄문에 빌드 시간을 단축할 수 있다`

**생성되는 결과물들은 어디에 저장될까?**

```
도커 컨테이너가 실행되면 모든 읽기 전용 레이어들을 순서대로 쌓은 다음 마지막에 쓰기 가능한 신규 레이어를 추가하게 된다. 그다음 컨테이너 안에서 발생하는 결과물들이 쓰기 가능 레이어를 기록되게 되는 것.
```

**컨테이너 업데이트**

![image](https://user-images.githubusercontent.com/55429912/121002492-5c8b8980-c7c7-11eb-90be-c5a43934e058.png)

1. 새 버전의 이미지를 다운(pull)
2. 기존 컨테이너를 삭제(stop, rm)
3. 새 이미지를 기반으로 새 컨테이너를 실행(run)

- **장점**

1. 애플리케이션 빠른 배포
   - 컨테이너 형식이 표준화 됨
2. 설치 및 확장이 쉽고, 이식성이 좋음
   - 다양한 인프라에 설치 가능
3. 오버헤드가 낮음
   - 하이퍼바이저 필요X
4. 관리가 쉬움
   - 수정된 부분만 소규모로 적용

---

### K8S

`쿠버네티스는 컨테이너화된 워크로드와 서비스를 관리하기 위한 이식성이 있고, 확장가능한 오픈소스 플랫폼`

---

## 리눅스

### 셸

명령어와 프로그램을 실행할 때 사용하는 인터페이스

- 커널과 사용자간의 다리역할

기능

- 사용자와 커널 사이에서 명령을 해석해 전달하는 **명령어 해석 기능**
- 셸은 자체 내에 **프로그래밍 기능**이 있어서 프로그램을 작성할 수 있음
  - 셸 프로그램을 셸 스크립트라고 부름
- 사용자 환경 설정의 기능
  - 초기화 파일 기능을 이용해 사용자의 환경을 설정할 수 있습니다.

### 프로세스

포그라운드 프로세스

- 사용자와 상호작용하는 프로세스

백그라운드 프로세스

- 사용자와 직접적인 대화를 하지 않고 뒤에서 실행되는 프로세스

데몬

- 리눅스 시스템이 부팅 시 자동으로 실행되는 백그라운드 프로세스
- 메모리에 상주하면서 사용자의 특정 요청이 오면 즉시 실행되는 대기중인 서버 프로세스이다

### 에디터

- 리눅스 편집기는 편집기를 통해 파일을 수정한다.
  - 원래 파일은 훼손되지 않게 남겨두고 해당 파일의 복사판을 만들어 임시 기억 장치에 둔다.
  - 임시 기억 장치는 편집기의 버퍼 역할을 한다.

---

## 캡스톤 디자인

### NodeMCU

`NodeMCU는 오픈소스 IoT플랫폼으로 와이파이 기능이 구현된 MCU 개발보드`

### Arduino IDE

`편집기, 컴파일러, 업로더 등이 합쳐진 소프트웨어 환경`

- 마이크로프로세스인 아두이노 보드를 인식하고 포트를 연결
- 아두이노를 제어하기 위한 소스 파일 작성
- 소스 파일을 아두이노에 업로드 가능한 기계어로 컴파일하여 업로드를 해주는 아두이노 전용 개발 프로그램

### GET & POST

**GET: 클라이언트에서 서버로 어떠한 리소스로부터 정보를 요청하기 위해 사용되는 메서드**

- GET 요청은 캐시가 가능
  - GET을 통해 서버에 리소스를 요청할 때 웹 캐시가 요청을 가로채 서버로부터 리소스를 다운로드하는 대신 리소스의 복사본을 반환한다. HTTP 헤더에서 cache-control헤더를 통해 캐시 옵션을 지정할 수 있다.
- GET 요청은 브라우저 히스토리에 남는다.
- GET 요청은 길이 제한이 있다
  - GET을 통한 요청은 URL 주소 끝에 파라미터로 포함되어 전송되기 때문에 길이에 제한이 있음
- GET은 데이터를 요청할때만 사용 된다.

**POST: 클라이언트에서 서버로 리소스를 생성하거나 업데이트하기 위해 데이터를 보낼때 사용되는 메서드**

- POST 요청은 캐시되지 않음
- POST 요청은 브라우저 히스토리에 남지 않음
- POST 요청은 데이터 길이에 제한이 없음
  - POST는 전송할 데이터를 HTTP 메시지 body 부분에 담아서 서버로 보내기 때문

**주요 차이점**

1. HTTP 메시지의 Body 유무
2. 사용 목적

---

## 시스템 프로그래밍

### 메모리 계층 구조

![image](https://user-images.githubusercontent.com/55429912/120774528-55614300-c55d-11eb-8599-8562317e0202.png)

- CPU가 데이터를 요청하면 메인 메모리에서 해당 데이터만 가져오는게 아닌 근접한 데이터들과 함께 블록 단위로 캐시로 가져옴(지역적 특성)
- 캐시에서 해당 데이터만 레지스터에게 전달
- 캐시에 요청 데이터 있을시 "캐시 히트", 없을 경우 "캐시 미스"

### 프로그램 최적화

- Code motion/ precomputation

  - 코드를 이동, 사전 계산하여 효율적인 실행 코드를 생성

  ```C
  // 코드 모션 전
  void set_row_before(double *a, double*b, long i, long n) {
     long j;
     for(j = 0; j < n; j++) {
        a[n * i + j] = b[j];
     }
  }
  ```

  ```C
  // 코드 모션 후
  void set_row_after(double *a, double*b, long i, long n) {
    long j;
    long ni = n * i;
    for(j = 0; j < n; j++) {
       a[ni + j] = b[j];
    }
  }
  ```

- Strength reduction

  - 무거운 연산을 가벼운 연산으로 바꾸는 컴파일러 최적화 기법
  - 곱하기,나누기 → 더하기,shift

  ```C
  // 연산자 변경 전
  for(i = 0; i < n; i++) {
     int ni = n * i;    // 곱하기 연산
     for(j = 0; j < n; j++) {
        a[ni + j] = b[j];
     }
  }
  ```

  ```C
  // 연산자 변경 후
  int ni = 0;
  for(i = 0; i < n; i++) {
     for(j = 0; j < n; j++) {
        a[ni + j] = b[j];
     }
     ni += n;
  }

  ```

- Sharing of Common subexpressions

  - 공통된 부분의 코드를 중복해서 실행하지 않는 기법

  ```C
  // 표현식 공유 전
  up = val[(i - 1) * n + j];
  down = val[(i + 1) * n + j];
  left = val[i * n + j - 1];
  right = val[i  * n + j + 1];
  sum = up + down + left + right;
  ```

  ```C
  // 표현식 공유 후
  int inj = i * n + j;
  up = val[inj - n];
  down = val[inj + n];
  left = val[inj - 1];
  right = val[inj + 1];
  sum = up + down + left + right;
  ```

### 링킹

![image](https://user-images.githubusercontent.com/55429912/120784737-5f883f00-c567-11eb-9b01-0ed42e6f9672.png)

`여러 개의 코드와 데이터를 모아서 연결하여 메모리에 로드될 수 있고 실행될 수 있는 한 개의 파일로 만드는 작업`

- 정적 링킹(Static Linking)

  - 실행 가능한 목적 파일을 만들 때 프로그램에서 사용하는 모든 라이브러리 모듈을 복사
  - 정적 링킹을 통해 만들어진 프로그램은 크기가 크고 메모리 효율이 좋지 않음
  - 특정 함수가 변경되면 그 변경을 적용하기 위해서 다시 컴파일하여 다시 링킹해야 함
  - 정적 링킹 라이브러리를 사용하는 프로그램은 동적 링킹 보다 빠름
  - 모든 코드가 하나의 실행 모듈에 담기기 때문에 불일치(Compatibility issues)에 대한 걱정을 하지 않아도 됨

- 동적 링킹(Dynamic Linking)
  - 실행 가능한 목적 파일을 만들 때 프로그램에서 사용하는 모든 라이브러리 모듈을 복사하지 않고 해당 모듈의 주소만을 가지고 있다가, 런타임에 실행 파일과 라이브러리가 메모리에 위치될 때 해당 모듈의 주소로 가서 필요한 것을 들고옴
  - 운영체제에 의해 이루어짐
  - 특정 함수의 주소만 가르키고 있기 때문에, 정적 링킹 방식에 비해 목적파일의 크기가 작다. 즉, **메모리와 디스크 공간을 더 아낄 수 있다.**
  - 특정 함수에 변화가 생겨도 **변화를 적용하기 위해 다시 컴파일하여 다시 링킹할 필요가 없음**
  - 동적라이브러리가 메모리에 이미 존재하는 경우 로드되는 시간을 단축시킬 수 있음
  - 매번 주소를 따라가야하는 **오버헤드가 존재**하기 때문에 정적 링킹 방식보다 느림
  - Compatibility issues 존재
  ```
  어떤 프로그램에서 A라는 함수를 동적 링킹 방식으로 사용하고 있을때, A라는 함수가 시스템에서 제거되면 이는 불일치 상황이다.
  해당 프로그램의 실행 가능 목적파일에는 A의 주소가 있어서 마치 A가 존재하는 것처럼 움직이지만 실제 A는 시스템에 더이상 존재하지 않기 때문이다.
  따라서 이 프로그램은 제대로 실행될 수 없다.
  ```

**링커**

- 링킹을 담당하는 프로그램
- 독립적인 컴파일을 가능하게 함

### Stack Overflow를 이용한 프로그램 해킹

`문자열의 최대 크기를 정하지 않는 특정 함수들의 특성을 이용하여 Stack영역의 돌아갈 곳의 주소(ret값)를 덮어 씌워 변경하는 것`

ASLR(Address Space Layout Randomization): 프로세스의 가상 주소공간에 어떤 object가 매핑될때, 그 위치 프로그램 실행시마다 랜덤하게 변경하는 보안 기법

---

## 데이터 통신

### ARP Spoofing

LAN에서 ARP를 이용하여 상대방의 데이터 패킷을 중간에서 가로채는 기법

`ARP(Address Resolution Protocol): IP주소를 MAC주소로 변환해주는 프로토콜`

![ARP spoofing](https://user-images.githubusercontent.com/55429912/119259472-7181ed80-bc09-11eb-981f-984831af3d44.png)

ARP 통신방법:

1. ARP는 기본적으로 MAC 주소를 얻기 위해 IP를 BroadCast방식으로 전송
2. 그 중에 필요한 MAC주소를 가지고 있는 특정 장치의 Response를 이용해 MAC 주소를 얻어냄
3. 받은 MAC 주소를 캐싱 테이블에 저장한 뒤, 이 주소를 이용하여 통신

**ARP Spoofing은 Broadcast로 전송된 IP요청을 받은 후 요청자에게 잘못된 MAC주소를 알려줌. 그리고 올바른 MAC주소를 가진 타겟 장치에 또한 요청자 MAC주소가 아닌 잘못된 MAC주소를 보내줌.**

**ARP과정이 매번 일어나면 망에 부담을 주지 않을까?**

![image](https://user-images.githubusercontent.com/55429912/121007701-1802ec80-c7cd-11eb-9800-7cd27aee3023.png)

ARP Table을 통해 해결

- ARP Table에 미리 IP와 MAC주소를 적어놓음
- ARP Table에 없으면 ARP과정을 수행
- CMD창에 arp -a를 통해 확인 가능
- 동적으로 저장된 것은 ARP reply에 의해 바뀔수 있음
- 정적으로 저장된 것은 사용자가 지우지 않는 한 고정

---

### 네트워크 공격 유형

1. 네트워크 공격

   ![image](https://user-images.githubusercontent.com/55429912/120896627-62fdf200-c65d-11eb-955f-bdddb0798c3b.png)

- 스니핑(Snipping): 네트워크상에서 전송되는 패킷을 캡쳐하여 이의 내용을 엿보는 행위
- 스푸핑(Spoofing): 데이터를 위/변조하여 다른 대상 시스템을 공격하는 기법
- 세션 하이재킹(Session Hijacking): 정상통신을 하고 있는 다른 사용자의 세션을 가로채서 별도의 인증 작업없이 가로챈 세션으로 통신을 계속하는 기법

2. 서비스 거부 공격

   ![image](https://user-images.githubusercontent.com/55429912/120896649-75782b80-c65d-11eb-9246-1e1082d6e940.png)

   - Dos(서비스 거부 공격):
   - 
     ![image](https://user-images.githubusercontent.com/55429912/121008790-56e57200-c7ce-11eb-939b-29b30be7d78f.png)

     타겟 시스템의 자원을 고갈시키거나 네트워크 대역폴을 초과시켜 원래 의도된 용도로 사용하지 못하게 하는 공격

   - DDos(분산 서비스 거부 공격):
   - 
     ![image](https://user-images.githubusercontent.com/55429912/121008731-47662900-c7ce-11eb-9043-f4aaa0dc9422.png)

     공격자가 여러 대의 컴퓨터를 감염시켜 동시에 한 타겟 시스템을 집중적으로 공격하는 기법

3. 네트워크 스캐닝 공격

   ![image](https://user-images.githubusercontent.com/55429912/120896689-95a7ea80-c65d-11eb-9e0e-eca76e2f3af9.png)

---

## 영상처리 & 머신러닝

### OpenCV

`Open Source Computer Vision, 다양한 영상처리에 사용할 수 있는 오픈소스 라이브러리`

- 무료
- C++, Python, java와 같은 다양한 인터페이스를 지원
- Windows, Linux, Mac OS등 다양한 OS를 지원
- 알고리즘 상으로 계산 효율성과 실시간 응용프로그램에 중점을 두고 설계되었기 때문에 간단하게 OpenCV에서 제공되는 API를 사용하여 코딩하여도 실시간 프로세싱이 가능한 어플리케이션을 만들 수 있기 때문에 최적화나 알고리즘을 생각하지 않고도 품질 좋은 상용프로그램을 만들 수 있음

### Dlib

`이미지 처리 및 기계 학습, 얼굴인식 등을 할 수 있는 C++로 개발된 고성능 라이브러리`

**dlib 라이브러리에서 얼굴 검출을 위한 방법**

1. HOG(Histogram of Oriented Gradients) 특성을 활용
   - dlib.get_frontal_face_detector()
    - 생성 객체: dlib.fhog_object_detector
2. 학습된 CNN모델을 사용
   - dlib.cnn_face_detection_model_v1(modelPath)
     - 생성 객체: mmod_rectangles 

얼굴검출기별 성능 비교: https://medium.com/nodeflux/performance-showdown-of-publicly-available-face-detection-model-7c725747094a

**HOG 특징**

`일반적으로 물체의 형태를 검출하거나, 사람의 형태를 검출하는 알고리즘`

![image](https://user-images.githubusercontent.com/55429912/121386664-26940400-c985-11eb-91fc-9d5a87ccd681.png)


1. 영상 또는 이미지 픽셀 값의 변화로 파악할 수 있는 영상 밝기 변화의 방향을 기울기 방향(gradient)값으로 표현
2. 해당 값을 통해 객체의 형태를 검출
   - 대상 영역을 일정 셀로 분할
   - 각 셀마다 Edge pixel들의 방향에 대한 histogram을 구함
   - 해당 값을 bin값으로 연결

**dlib 라이브러리에서 얼굴 인식을 위한 방법**

얼굴 검출기를 통해 검출된 얼굴은 해당 인물의 고개의 각도나 시선의 방향으로 인해 서로 다른 사람으로 인식 될 수 있음

face landmark estimation 알고리즘
- 기본적인 접근방식은 모든 얼굴에 존재하는 랜드마크를 찾는 것 

**i·bug 300-W**

300-W Data set은 i·bug(intelligent behaviour understanding group)에서
연구 목적으로 제공되는 Data set이다.

### CMake

`멀티 플랫폼을 위한 빌드 지원 시스템`

- **정적 및 동적 라이브러리 빌드 지원**
- 네이티브 빌드 환경을 생성할 수 있음

### 문제점 및 해결법 

1. Python 지원 오류
    ```
    dlib의 import오류를 해결하기 위해 공식 래퍼런스를 참조하여 확인해 본 결과 dlib 라이브러리는 C++로 작성된 툴킷이기에 다른 인터페이스에서 사용하려면 컴파일을 해야함.
    ```
    
    해결법:
    ```
    공식 레퍼런스에서 CMake를 이용하여 컴파일하는 것을 권장하여 CMake를 이용하여 dlib를 컴파일 한 후 사용
    ```

2. 얼굴 정면으로 구성된 Datasets
    ```
    얼굴 인식기 shape_predictor()에 Dataset인 "shape_predictor_68_face_landmarks.dat"를 사용하여 얼굴에 랜드마크 설정시 정면얼굴로 구성된 데이터 셋으로 인해 옆모습일 경우 얼굴검출을 되지만 랜드마크 설정이 되지 않음
    ```

    해결법:
    ```
    초기 얼굴에 랜드마크 설정된 좌표값을 저장하고 해당 좌표값의 이동 비율과 시간을 통해 옆모습을 예측
    ```

3. 디자인과 유지보수성
    ```
    기능뿐인 프로그램이라 디자인적 미적요소가 낮음, 웹서비스와 접목하여 유지보수성을 높이고 싶음
    ```

    해결법:
    ```
    웹개발지식(프론트랑 백 모두) 배우고 웹이랑 연동해서 리팩토링 할 것임..
    ```

---

## Back-End

### Spring

POJO(Plain Old Java Object): 특정프레임워크나 기술에 종속적이지 않은 자바 객체

PSA(Portable Service Abstraction): 일관된 방식으로 기술에 접근할 수 있게 해주는 설계 원칙

IoC/DI(Dependency Injection): 객체 간의 의존 관계를 외부에서 다이나믹하게 설정

AOP(Aspect Oriented Programming): 관심사의 분리를 통한 SW의 모듈성 향상

---

## Front-End

- Vue
