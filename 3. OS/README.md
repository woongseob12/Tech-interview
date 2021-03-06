# OS

`하드웨어를 관리, 응용 프로그램과 하드웨어 사이에서 인터페이스 역할을 하며 시스템의 동작을 제어하는 시스템 소프트웨어`

## 프로세스란?

`실행 중인 프로그램(= 스케줄링의 대상이 되는 작업)`

- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립적인 개체)
- OS로 부터 시스템 자원을 할당받는 작업의 단위
- 하드디스크에 있는 프로그램을 실행하면, 실행을 위해서 메모리 할당이 이루어지고, 할당된 메모리 공간으로 바이너리 코드가 올라가게 됨. 이 순간부터 **프로세스**라고 부름.

- 할당받는 시스템 자원

  - CPU 시간
  - 운영되기 위해 필요한 주소 공간
  - Code, Data, Stack, Heap의 구조로 되어 있는 독립된 메모리 영역

- 메모리 구조

  - Code 영역: 프로그램을 실행시키는 실행 파일 내의 명령어 할당
  - Data 영역: 전역변수, static 변수 할당
  - Heap 영역: 동적 할당을 위한 메모리 영역
  - Stack 영역: 지역변수, 매개변수, 리턴값 등을 위한 메모리 영역

- 특징

  - 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap)을 할당 받는다.
    ![process](https://user-images.githubusercontent.com/55429912/120060193-47a94a80-c091-11eb-8dd4-7e49dca2302f.png)
  - 프로세스당 최소 1개의 스레드를 보유
  - 각 프로세스는 별도의 주소 공간에서 실행되며, 한 프로세스가 다른 프로세스의 자원에 접근하려면 IPC(Inter-process communication, 프로세스 간의 통신)를 사용해야 한다.

## 멀티 프로세스란?

`두개 이상의 프로세서(CPU)가 하나 이상의 작업을 동시에 처리하는 것(병렬처리)`

장점: 안정성(메모리 침범 문제를 OS차원에서 해결)

- 여러 개의 프로세서에 분산한다면, 한 프로세서가 고장나더라도 시스템이 정지하는 것이 아닌 속도만 느려지게 된다.

단점: 작업량이 많을수록 오버헤드 발생, Context Switching으로 인한 성능 저하

`오버헤드: 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간, 메모리 등`

## 스레드란?

`프로세스 내에서 실행되는 여러 흐름의 단위`

- 특징

  - 스레드는 프로세스내의 Code, Data, Heap영역은 공유하며 Stack영역만 따로 할당 받는다.
    ![thread](https://user-images.githubusercontent.com/55429912/120063107-82ff4580-c0a0-11eb-9e90-69ae93b72239.png)

  - 스레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, 프로세스 내의 주소 공간이나 자원들을 공유하며 실행된다.
  - 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드(sibling thread)도 그 변경 결과를 즉시 볼 수 있다.

- 장점
  - 메모리 공유로 인한 시스템 자원 소모가 줄어듦
  - 응답시간 단축
  - Context Switching에 대한 오버헤드가 줄어듦(Stack영역만 switching하면 되기 때문)
- 단점
  - 자원 동기화에 신경써야 함

## 멀티 스레드란?

`하나의 응용 프로그램에서 여러 스레드를 구성해 각 스레드가 하나의 작업을 처리하는 것`

스레드들이 공유 메모리를 통해 다수의 작업을 동시에 처리하도록 해줌

장점: 독립적인 프로세스에 비해 공유 메모리만큼의 시간, 자원 손실이 감소, 전역 변수와 정적 변수에 대한 자료 공유 가능

단점: 안정성 문제. 하나의 스레드가 데이터 공간을 망가뜨리면, 모든 스레드가 작동 불능(공유 메모리를 갖기 때문)

## 멀티 스레드가 멀티 프로세스보다 좋은 이유?

- 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 **자원을 효율적으로 관리**할 수 있음
  - 프로세스간의 Context Switching의 경우 캐시 메모리에 대한 데이터까지 초기화 되므로 오버헤드가 커짐
- 프로세스 간의 통신(IPC)보다 스레드 간의 통신 비용이 적고, 전환 속도가 빨라 작업들 간의 **처리 비용 감소 및 응답 시간 단축**
  - 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문
  - Context Switching시 스레드는 Stack 영역만 처리하기 때문

그렇다면 왜 멀티스레드만 사용하지 멀티프로세스를 쓰느냐? ☞

**스레드간의 자원 공유는 전역 변수를 이용하므로 동기화 문제에 신경써야 함**

---

## 임계영역(Critical section)이란?

`둘 이상의 스레드가 동시에 접근해서는 안되는 공유 자원을 접근하는 코드의 일부`

**임계 영역 문제란?**

`프로세스들이 임계 영역을 동시에 접근하였을 때 발생하는 동기화 문제`

**임계 영역 문제를 해결하기 위한 기본 조건**

1. 상호배제(Mutual Exclution): 하나의 프로세스가 임계 영역에 들어가 있다면 다른 프로세스는 들어갈 수 없어야 한다.
2. 진행(Progress): 임계 구역에 들어간 프로세스가 없는 상태에서, 들어가려고 하는 프로세스가 여러 개 있다면 어느 것이 들어갈지를 적절히 결정해주어야 한다.
3. 한정된 대기(Bounded Waiting): 다른 프로세스의 Starvation을 방지하기 위해, 한 번 임계 구역에 들어간 프로세스는 다음 번 임계 구역에 들어갈 때 제한을 두어야 한다.

## Thread-safe란?

`멀티스레드 환경에서 여러 스레드가 동시에 공유 자원에 접근할 때, 의도한 대로 동작하는 것`

- 상호배제: Thread-safe하기 위해서는 공유 자원에 접근하는 임계영역(critical section)을 동기화 기법으로 제어(Ex. Mutex, Semaphore)
- Re-entrancy: 어떤 함수가 한 스레드에 의해 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하더라도 그 결과가 각각에게 올바르게 주어져야 함
- Thread-local storage
  - 공유 자원의 사용을 최대한 줄이고 각각의 스레드에서만 접근 가능한 저장소들을 사용함으로써 동시 접근을 막는다.
- Atomic operations
  - 데이터 변경시 atomic하게 데이터에 접근하도록 만듦

## 동기화 객체

스레드 동기화 방법

- 실행 순서의 동기화
  - 스레드의 실행순서를 정의하고, 이 순서에 반드시 따르도록 하는 것
- 메모리 접근에 대한 동기화
  - 메모리 접근에 있어서 동시접근을 막는 것
  - 실행의 순서가 중요한 상황이 아니고, 한 순간에 하나의 스레드만 접근하면 되는 상황

동기화 기법의 종류

1. 유저 모드 동기화
   `성능상 이점, 기능 적음(라이브러리를 이용)`

- 커널의 코드가 실행되지 않는 동기화 기법
- 성능상 이점이 있으나, 기능상의 제한점이 존재
- 임계 구역 기반의 동기화, 인터락 함수 기반의 동기화

2. 커널 모드 동기화
   `기능상 우수, 속도 떨어짐. 각 프로세스들 안에 있는 스레드끼리의 동기화도 가능`

- 커널에서 제공하는 동기화 기능을 이용
- 커널 모드로의 변경이 필요하고 이는 성능 저하로 이어짐.
  - But, 다양한 기능을 활용할 수 있다.
- 세마포어, 뮤텍스, 모니터 등..

<table border="2">
  <tr>
    <th>모드</th>
    <th>이름</th>
    <th>사용</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>유저</td>
    <td>크리티컬 섹션 기반 동기화</td>
    <td>메모리 접근 동기화에 사용</td>
    <td>크리티컬 섹션 오브젝트(자료형이 CRITICAL_SECTION인 변수)를 만들고 초기화</td>
  </tr>
  <tr>
    <td>유저</td>
    <td>인터락 함수 기반 동기화</td>
    <td>메모리 접근 동기화에 사용</td>
    <td>함수 내부적으로 한 순간에 하나의 쓰레드에 의해서만 실행되도록 동기화</td>
  </tr>
  <tr>
    <td>커널</td>
    <td>뮤텍스 기반 동기화</td>
    <td>메모리 접근 동기화에 사용</td>
    <td>키의 취득과 반납이 이루어짐(동기화 대상이 하나)</td>
  </tr>
  <tr>
    <td>커널</td>
    <td>세마포어 기반 동기화</td>
    <td>메모리 접근 동기화에 사용</td>
    <td>카운트를 통해 이루어짐(동기화 대상이 하나 이상)</td>
  </tr>
  <tr>
    <td>커널</td>
    <td>이름있는 뮤텍스 기반 동기화</td>
    <td>프로세스간 동기화에 사용</td>
    <td>프로세스 동기화를 하기 위해서 뮤텍스를 동기화 해야하는데 커널 오브젝트는 각각 프로세스에 독립적이므로 뮤텍스에 이름을 붙여서 접근</td>
  </tr>
  <tr>
    <td>커널</td>
    <td>이벤트 기반 동기화</td>
    <td>실행순서 동기화에 사용</td>
    <td></td>
  </tr>
</table>
<br>

---

## 세마포어(Semaphore) & 뮤텍스(Mutex)

**세마포어란?**

```
공유된 자원의 데이터 혹은 임계영역에 여러 프로세스 혹은 스레드가 접근하는 것을 막는 것
(동기화 대상이 하나 이상)
```

- 공유 리소스에 접근할 수 있는 프로세스의 최대 허용치만큼 동시에 사용자가 접근하여 사용할 수 있다.
- 각 프로세스는 세마포어 값을 확인하고 변경할 수 있다.
- 현재 수행중인 프로세스가 아닌 다른 프로세스가 세마포어를 해제할 수 있다.

**뮤텍스란?**

```
공유된 자원의 데이터 혹은 임계영역에 하나의 프로세스 혹은 스레드가 접근하는 것을 막는 것`
(동기화 대상이 하나)
```

- 다중 프로세스들의 공유 리소스에 대한 접근을 조율하기 위해 lock/unlock을 사용
  - ex) Linux에서의 Mutex는
  ```c
  while(1) {
    pthread_mutex_lock(&mutex);   // lock
    // critical section
    pthread_mutex_unlock(&mutex); // unlock
  }
  ```
- 뮤텍스는 lock을 획득한 프로세스(혹은 스레드)가 반드시 해당 lock을 unlock해야 한다.

**Atomic Opretaion**

`실행 중에 중단하지 않는 순차적인 기계어 명령`

세마포어 실행시에는 Atomic Opretaion이여야 함

atomic instruction이 아닐 경우 → 명령어 도중 인터럽트가 발생 될 수 있음 → context switching이 발생할 수 있음 → 동시 접근을 허용할 수도 있음 → 공유 자원 충돌 문제가 날 수 있음


**차이점**

- **관리하는 동기화 대상의 개수**
  - 세마포어: 동기화 대상이 한개 이상
  - 뮤텍스: 동기화 대상이 한개
- 뮤텍스의 경우 뮤텍스를 소유하고 있는 스레드가 해당 뮤텍스를 해제할 수 있다.
- 세마포어는 세마포어를 소유하지 않는 스레드가 세마포어를 해제할 수 있다.

---

## 동기와 비동기

**동기(Synchronous)란?**

`어떤 작업을 요청했을 때, 그 작업이 종료될 때까지 기다린 후 다음 작업을 수행`

- 데이터를 주고받는 **순서**가 중요할 때 사용
- 요청한 작업만 처리하면 되기 때문에 전체적인 수행 속도는 빠를 수 있음
- 한 작업에 대한 시간이 길어질 경우, 전체 응답이 지연될 수 있다.

**비동기(Asynchronous)란?**

`어떤 작업을 요청했을 때, 그 작업이 종료될 때까지 기다리지 않고(작업을 위임하고) 다음 작업을 수행`

- 요청 순서에 상관없이, 동시에 다수의 작업을 처리할 수 있음
- 작업이 끝날 때 따로 이벤트를 감지하고 결과를 받아 그에 따른 추가 작업을 해줘야하기 때문에, 비교적 느릴 수 있다.
- I/O 작업이 잦고, 빠른 응답속도를 요구하는 프로그램에 적합

**Blocking vs Non-Blocking**

Bloking I/O Model

- 시스템 콜이 끝날때까지 프로그램은 대기해야 하고 시스템콜이 완료되면 그때 Return
  - ex. C언어의 scanf()
- Wait Queue에 들어감

Non-Bloking I/O Model

- 시스템 콜이 끝나지 않아도 대기하지 않고 Return
- Wait Queue에 들어가지 않음

**차이점**

1. Blocking vs Non-Blocking

- Blocking: 프로그램이 바로 실행할 수 없음
- Non-Blocking: 프로그램이 바로 실행할 수 있음

2. 동기 vs 비동기

- 동기: 시스템 콜이 끝날때까지 기다림
- 비동기: 시스템 콜이 완료되지 않아도 나중에 완료되면 그때 결과물을 가져옴

3. Non-Blocking vs 비동기

- Non-Blocking: 요청에 처리할 수 있으면 바로 응답, 아닐 경우 Error 반환
- 비동기: 요청에 처리 완료와 관계없이 응답

4. Blocking vs 동기

- Blocking: 시스템 콜이 return을 기다리는 동안 필수로 Wait Queue에 대기
- 동기: 시스템 콜이 return을 기다리는 동안 Wait Queue에 대기할 수도 안할 수도 있음

[출처] https://velog.io/@wonhee010/%EB%8F%99%EA%B8%B0vs%EB%B9%84%EB%8F%99%EA%B8%B0-feat.-blocking-vs-non-blocking
---

## 인터럽트(Interrupt)

`CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치에 예외상황이 발생하여 처리가 필요한 경우에 CPU에게 알려 처리할 수 있도록 하는 것`

**인터럽트는 왜 할까?**

`입출력 연산이 CPU 명령 수행속도보다 현저히 느리기 때문`

종류

- 하드웨어 인터럽트
  - CPU가 아닌 다른 하드웨어 장치가 CPU에 어떤 사실을 알려주거나, CPU 서비스를 요청해야할 경우 발생
- 소프트웨어 인터럽트
  - 소프트웨어가 스스로 인터럽트 라인을 세팅
  - ex. 예외 상황, System call

**인터럽트를 발생 시키기 위해 HW/SW는 CPU내에 있는 인터럽트 라인을 세팅하여 인터럽트를 발생시킨다.**

**CPU는 매번 명령을 수행하기 전에 인터럽트라인이 세팅되어있는지를 검사한다.**

**과정**

![인터럽트](https://user-images.githubusercontent.com/55429912/120112394-94377780-c1b0-11eb-8277-e390ea0cc243.png)

상태 레지스터와 PC등을 스택에 잠시 저장한 뒤 인터럽트 서비스 루틴으로 이동
(인터럽트 서비스 루틴이 끝난 뒤 다시 원래 작업으로 돌아오기 위해!)

**만약 인터럽트 기능이 없다면?**

`컨트롤러는 특정한 어떤일을 할 시기를 알기 위해 계속 체크를 해야함(폴링 방식)`

**인터럽트와 특권 명령**

CPU 명령어의 종류

1. 일반 명령
   - 메모리에서 자료를 읽고, CPU에서 계산을 하는 등의 명령
   - 모든 프로그램이 수행할 수 있는 명령
2. 특권 명령
   - 입출력 장치, 타이머 등의 장치를 접근하는 명령
   - 보안이 필요한 명령으로 항상 **운영체제**만이 수행할 수 있다.

**관련 용어**

- 인터럽트 핸들러(= 인터럽트 서비스 루틴): 실제 인터럽트를 처리하기 위한 루틴, 운영체제의 코드 영역에는 인터럽트별로 처리해야할 내용이 이미 프로그램 되어 있음

- 인터럽트 벡터: 인터럽트 발생시 처리해야할 인터럽트 핸들러의 주소를 인터럽트 별로 보관하고 있는 테이블

---

## PCB(Process Control Block)

**PCB(Process Control Block)란?**

`프로세스 메타데이터들을 저장해 놓는 곳`

- 한 PCB안에는 한 프로세스의 정보가 담김
- 커널의 데이터 영역에 존재
- 인터럽트 발생 시 프로세스의 메타데이터들을 저장

**PCB가 필요한 이유?**

`다시 수행할 프로세스의 상태값을 PCB에 저장해두기 위해`

**PCB 관리 방법?**

`Linked List방식으로 관리`

PCB List Head에 PCB들이 생성될 때 마다 붙게된다. 주소값으로 연결이 이루어져 있는 연결리스트이기 때문에 삽입, 삭제가 용이하다.

**즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스가 완료되면 제거된다.**

---

## Context Switching

**Context Switching이란?**

`현재 진행하고 있는 작업(프로세트, 스레드)의 상태를 저장하고 다음 진행할 작업의 상태 값을 읽어 적용하는 과정`

**왜 Context Switching이 필요한가?**

- Computer가 매번 하나의 Task만 처리할 수 있다면?
  - 해당 Task가 끝날때까지 다음 Task는 기다릴 수 밖에 없음
  - 또한 반응속도가 매우 느리고 사용하기 불편
- 다양한 사람들이 동시에 사용하는 것처럼 사용하기 위해선?
  - 멀티태스킹을 통해 빠른 반응속도로 응답할 수 있음
  - 빠른 속도로 Task를 바꿔가며 실행하기 떄문에 사람의 눈으론 실시간처럼 보임
  - **CPU가 Task를 바꿔가며 실행하기 위해 Context Swtiching 필요**

**Context Switching 과정**

1. Task의 대부분 정보는 레지스터에 저장되고, PCB(Process Control Block)로 관리된다.

  ![pcb](https://user-images.githubusercontent.com/55429912/120107634-c6d77500-c19c-11eb-9f74-3bb2e75b4b86.png)

  **[PCB 구조]**

2. 현재 실행하고 있는 Task의 PCB정보를 저장한다.
3. 다음 실행할 Task의 PCB정보를 읽어 레지스터에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있다.

**Context Switching 비용**

- Cache 초기화
- Memory Mapping 초기화
- Kernel은 항상 실행되어야 함(메모리의 접근을 위해서)

Process > Thread

Thread는 Stack 영역을 제외한 모든 메모리를 공유하므로, Context Switching 수행 시 Stack영역만 변경하면 되기 때문

---

## IPC(Inter-Process Communication)

**IPC란?**

`프로세스간 통신`

![리눅스 커널 구조](https://user-images.githubusercontent.com/55429912/120153217-69d5d080-c229-11eb-93ec-2e001d9e48ca.png)

[리눅스 커널 구조]

- 프로세스는 독립적으로 실행
- 독립된 구조인 만큼 별도의 설비가 없이 서로 간의 통신이 어려움

**IPC 종류**

<table border="2">
  <tr>
    <th style="text-align:center">이름</th>
    <th style="text-align:center">사용</th>
    <th style="text-align:center">특징</th>
  </tr>
  <tr>
    <td>익명 PIPE</td>
    <td>
      통신을 할 프로세스가 명확하게 알수 있는 경우<br>(부모 - 자식 프로세스)
    </td>
    <td>
      <ul>
        <li>
          한쪽 방향으로만 통신 가능한 <strong>Half-Duplex(반이중)통신</strong>
        </li>
        <li> 
        Full-Dulpex(전이중) 통신을 하기 위해서는 2개의 PIPE가 필요        
        </li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>Named PIPE(FIFO)</td>
    <td>
      전혀 모르는 상태의 프로세스들 사이의 통신
    </td>
    <td>
      <ul>
      <li>
        프로세스 통신을 위해 이름이 있는 파일을 사용
      </li>
        <li> 
        Named PIPE의 생성은 mkfifo를 통해 이루어지며, mkfifo가 성공하면 명명된 파일이 생성됨
        </li>
        <li> 
        Full-Dulpex(전이중) 통신을 하기 위해서는 2개의 PIPE가 필요        
        </li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Message Queue</td>
    <td>메모리 공간으로 사용</td>
    <td>
      <ul>
        <li>메시지 큐에 사용할 데이터를 라벨링함으로써 여러 개의 프로세스가 데이터를 쉽게 다룰 수 있음 </li>
        <li>커널에서 관리</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Shared Memory</td>
    <td>메모리를 공유</td>
    <td>
      <ul>
        <li>프로세스간 메모리 영역을 공유해서 사용할 수 있도록 허용</li>
        <li>IPC들 중에서 가장 빠르게 작동(중재자가 없기 때문)</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Memory Map</td>
    <td>메모리를 공유</td>
    <td>
      <ul>
        <li>오픈된 파일에 한해서 메모리에 맵핑시켜 공유
        <br>(Shared Memory와의 차이점)</li>
        <li>메모리의 내용을 파일로 남길수 있음</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Semaphore</td>
    <td>프로세스간 데이터를 동기화 및 보호</td>
    <td>
      <ul>
        <li>Busy wait 상태에 놓이지 않음</li>
        <li>커널에서 관리되기 때문에 다른 프로세스들 간에도 사용 가능</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Socket</td>
    <td>물리적으로 떨어져 있는 컴퓨터간의 통신</td>
    <td>
      <ul>
        <li>네트워크 통신에 사용하던 기술을 그대로 사용 가능</li>
        <li>규모가 클 경우 효율적</li>
      </ul>
    </td>
  </tr>
</table>

**커널이란?**

`메모리에 상주하는 운영체제의 부분`

- 운영체제 자체도 소프트웨어로서 메모리에 프로그램이 올라가야함
- 운영체제는 규모가 큰 프로그램으로 모두 메모리에 올라간다면 한정된 메모리 공간의 낭비가 심함

---

## 시스템 콜(System Call)

**운영체제의 두가지 Operation**

운영체제는 하드웨어적인 보안을 유지하기 위해 기본적으로 두가지 Opreation을 지원

1. Kernel mode(모드비트 = 0): 운영체제가 CPU의 제어권을 가지고 명령을 수행하는 모드로 **일반 명령**과 **특권 명령** 모두 수행할 수 있음
2. User mode(모드비트 = 1): 일반 사용자 프로그램이 CPU제어권을 가지고 명령을 수행하는 모드이기 때문에 **일반 명령**만을 수행할 수 있음

![syscall](https://user-images.githubusercontent.com/55429912/120147817-3cd1ef80-c222-11eb-8392-7a5acfa6ea29.png)

1. CPU가 인터럽트 라인이 세팅되었는지 검사(매 명령 실행 전)
2. 인터럽트 발생한 것을 감지하면, 현재 수행중인 사용자 프로그램을 멈추고 CPU의 제어권을 OS에게 양도(Kernel mode)
3. 하드웨어적으로 모드 비트가 1에서 0으로 자동으로 세팅되어 특권 명령을 수행할 수 있게 됨

`시스템 콜은 커널 영역의 기능을 사용자 모드가 사용 가능하게, 즉 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게 해준다.`

fork(), exec(), wait()와 같은 것들은 Process 생성과 제어를 위한 System call

fork(): 새로운 Process를 생성(새로운 Process를 위한 메모리를 할당)

```
Parent의 fork() 값 => child의 PID값
Child의 fork() 값 => 0
```

`Scheduler가 부모 프로세스를 먼저 수행할지 자식 프로세스를 먼저 수행할지 확신할 수 없음`

exec(): 새로운 Process를 생성(부모 프로세스의 메모리에 자식 프로세스의 코드를 덮어씌움)

```C
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146

    int rc = fork();				    // 주목

    if (rc < 0) {
        exit(1);                        // (1) fork 실패
    }
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
        char *myargs[3];
        myargs[0] = strdup("wc");		// 내가 실행할 파일 이름
        myargs[1] = strdup("p3.c");		// 실행할 파일에 넘겨줄 argument
        myargs[2] = NULL;				// end of array
        execvp(myarges[0], myargs);		// wc 파일 실행.
        printf("this shouldn't print out") // 실행되지 않음.
    }
    else {								// (3) parent case
        int wc = wait(NULL)				// 추가된 부분
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```

exec()가 실행되면, execvp(실행 파일, 전달 인자) 함수는 Code 영역에 실행 파일의 코드를 덮어 씌움. 그로 인해 execvp()이후의 부분은 실행되지 않음

wait(): Child 프로세스가 종료될 때까지 대기

```
int wc = wait(NULL); // wait()함수를 추가하여 자식프로세스 종료를 대기
```

## 데드락(교착상태, Deadlock)

**교착상태란?**

`두 개 이상의 작업이 서로 상대방의 작업이 끝나기만을 기다리고 있기 때문에 아무것도 완료되지 못하는 상태, 즉 프로세스가 자원을 얻지 못해 다음 처리를 하지 못하는 상태`

**교착상태 조건**

1. 상호배제(Mutual Exclusion)

   `한 번에 한 프로세스만 공유 자원을 사용할 수 있다.`

2. 점유대기(Hold and Wait)

   `공유 자원에 대한 접근 권한을 갖고 있는 프로세스가, 그 접근 권한을 양보하지 않은 상태에서 다른 자원에 대한 접근 권한을 요구할 수 있다.`

3. 비선점(No Preemption)

   `한 프로세스가 다른 프로세스의 자원 접근 권한을 강제로 취소할 수 없다.`

4. 순환대기(Circular Wait)

   `두 개 이상의 프로세스가 자원 접근을 기다리는데, 그 관계에 사이클이 존재한다.`

**교착 상태 처리**

1. 예방

- 상호배제 부정: 여러 프로세스가 공유 자원을 사용
- 점유대기 부정: 프로세스 실행 전 모든 자원을 할당
- 비선점 부정: 자원 점유 중인 프로세스가 다른 자원을 요구할 때 가진 자원 반납
- 순환대기 부정: 자원에 고유 번호 할당 후 순서대로 자원 요구

2. 회피

- 은행원 알고리즘:
  - 시스템은 자원을 할당한 후에도 안정 상태로 남아있는지 사전에 검사
  - 안정 상태면 자원 할당, 아니면 다른 프로세스들이 자원 해지까지 대기
    - 안정 상태(safe state): 시스템이 교착상태를 일으키지 않으면서 각 프로세스가 요구한 최대 요구량 만큼 필요한 자원을 할당해 줄 수 있는 상태
    - 불안전 상태(unsafe state): 프로세스의 자원 할당 및 해제의 순서가 불명확하여 교착상태의 발생 가능성이 있는 상태
  
3. 탐지 & 회복

- 자원 할당 그래프를 통해 교착 상태를 탐지
- 자원 요청시, 탐지 알고리즘을 실행시켜 교착상태 확인(오버헤드 발생)

- 교착 상태를 일으킨 프로세스를 종료 하거나, 할당된 자원을 해제시켜 회복시키는 방법
  - 프로세스를 종료하는 법
    - 교착 상태의 프로세스를 모두 중지
    - 교착 상태가 제거될 때까지 하나씩 프로세스 중지
  - 자원을 선점하는 법
    - 교착 상태의 프로세스가 점유하고 있는 자원을 선점하여 다른 프로세스에게 할당하며, 해당 프로세스를 일시 정지시키는 방법
    - 우선순위가 낮은 프로세스, 수행된 횟수가 적은 프로세스 등을 위주로 프로세스의 자원을 선점

**식사하는 철학자 문제**

- 문제점

  1. 상호배제: 젓가락은 한번에 한 철학자만 사용할 수 있다.
  2. 점유대기: 집어든 젓가락은 계속 집은채로 반대쪽 젓가락을 기다린다.
  3. 비선점: 이미 누군가 집어든 젓가락을 강제로 뺏을 수 없다.
  4. 순환대기: 모든 철학자들이 자신의 오른쪽에 앉은 철학자가 젓가락을 놓기를 기다린다.

- 해결법
  1. N명이 앉을 수 있는 테이블에서 N - 1명만 앉힘
     (은행원 알고리즘인가..? )
  2. 두개의 젓가락을 모두 집을 수 있는 상황에서만 젓가락을 집도록 허용(점유대기 부정)
  3. 누군가는 왼쪽 젓가락을 먼저 집지 않고 오른쪽 젓가락을 먼저 집도록 허용(순환대기 부정)

---

## CPU Scheduling

**스케줄링이란?**

`메모리에 올라온 프로세스들 중 어떤 프로세스를 먼저 처리할지 일들의 순서를 정하는 일`

효율성 ⇒ CPU 사용률,처리율 ↑/ 반환시간, 대기시간, 반응시간 ↓
<br>
공평성 ⇒ 각 기준에 있어 최적의 평균값과 이들 간의 편차를 최소화
<br>
대화형 시스템 ⇒ 반응시간의 편차가 적은 스케줄러 선정

장기 스케줄러(long term scheduler, 또는 작업 스케줄러)

`메모리와 디스크 사이의 스케줄링`

- 스케줄러 원칙에 따라 디스크 내의 작업을 어떤 순서로 메모리에 가져올지 결정
- 디스크와 같은 저장장치에 작업들을 저장해 놓고, 필요할 때 실행할 작업을 ready queue에서 꺼내 메모리에 적재
- New → Ready/ Running(or Ready) → Terminated

단기 스케줄러(short term scheduler, 프로세스 스케줄러, CPU 스케줄러)

`CPU와 메모리 사이의 스케줄링`

- 메모리에 있는 프로세스 중 하나를 선택해 프로세서를 할당
- Ready → Running → Waiting → Ready

**종류**

1. 비선점 스케줄링

`할당된 CPU를 다른 프로세스가 강제로 빼앗아 사용할 수 없는 스케줄링`

- CPU를 할당받은 프로세스가 종료되거나 입출력 조작을 위해 자발적으로 중지되기 전까지 CPU할당을 보장하는 스케줄링
  - FIFO(=FCFS): 준비 큐에 도착한 순서로 CPU를 할당
  - SJF(Short Job First): 준비 큐에 있는 프로세스들 중에 실행시간이 가장 짧은 프로세스에 CPU를 할당
  - 비선점 우선순위: 각 프로세스에 우선순위를 부여하여 우선순위가 높은 순서대로 CPU를 할당
  - HRN(Highest Response Ratio Next): SJF의 기아 현상을 에이징기법으로 보완한 방법

2. 선점 스케줄링

`우선순위가 높은 다른 프로세스가 CPU를 강제로 빼앗아 사용할 수 있는 스케줄링`

- 비선점 스케줄링의 경우 응답시간이 예상이 되는 장점이 있지만 중요한 일이 중요하지 않은 일을 기다리는 경우가 발생할 수 있음

  - RR(Round Robin): 시간 할당량 동안만 실행한 후 완료되지 않으면 다음 프로세스에게 CPU를 양보하고 준비 큐의 가장 뒤로 배치

    ![라운드로빈](https://user-images.githubusercontent.com/55429912/120168491-e07aca00-c239-11eb-9d3b-baf34ace5970.png)

    - TQ(Time Quantum, 시간 할당)이 클수록 FIFO와 유사, 작을 수록 Context Switching이 잦아짐에 따라 오버헤드 발생

  - SRT(Shortest Remaining Time): 최단 잔여시간을 우선으로 하는 스케줄링
  - 선점 우선순위: 우선순위가 높은 순서대로 CPU를 할당, 준비 큐에 새로 들어온 프로세스의 우선순위가 현재 프로세스보다 높을 경우 CPU를 새로운 프로세스에게 할당

  - MLQ(Multilevel Queue, 다단계 큐): 커널 내의 준비 큐를 여러개의 큐로 분리하여 큐 사이에도 우선순위를 부여하는 스케줄링 알고리즘
    ![MLQ](https://user-images.githubusercontent.com/55429912/120174111-b1ffed80-c23f-11eb-9724-e80b05336d08.png)

    - 정적 우선순위를 사용하는 스케줄링을 구현할 때 가장 적합한 자료구조
    - 우선순위마다 준비 큐 형성(우선순위크기 만큼의 준비큐 필요)
    - 항상 가장 높은 우선순위 큐의 프로세스에 CPU를 할당(우선순위가 낮은 큐에서 작업이 실행중이더라도 상위 단계의 큐에 프로세스가 도착하면 CPU를 뺏기는 선점 방식)
    - 각 큐는 독자적 스케줄링 사용 가능
    - 큐들 간의 프로세스 이동이 불가능
    - 기아현상 발생할 수 있음

  - MFQ(Multilevel Feedback Queue, 다단계 피드백 큐): 다단계 큐라는 스케줄링에서 피드백이 추가된 스케줄링

    ![MFQ](https://user-images.githubusercontent.com/55429912/120177565-87b02f00-c243-11eb-9379-6167a43d6fd4.png)

    - CPU burst와 중요도의 상관관계
  
      `CPU Burst란? 프로그램의 수행중에 연속적으로 CPU를 사용하는 단절된 구간, 스케줄링의 단위가 된다`
    - 사용자와 Interactive ⇒ CPU Burst ↓
    - Background 프로세스 ⇒ CPU Burst ↑
    - TQ를 다 채웠다는 것은 CPU Bound prcess일 가능성이 높으므로 한단계 밑으로 내림
    - 높은 우선순위일수록 TQ가 짧고, 낮은 우선순위일수록 TQ가 김
    - 기아현상을 에이징 기법으로 예방

**MLQ와 MFQ의 차이점?**

1. 큐와 큐사이에 프로세스들의 이동가능 여부

- MLQ: 불가능, 스케줄링 부담이 적지만 유연성은 떨어짐
- MFQ: 가능

2. 기아현상

- MLQ: 하위 단계의 큐에 있을수록 CPU 할당을 받지 못하여 기아현상이 발생할 수 있음
- MFQ: 에이징 기법을 통해 기아 현상을 예방할 수 있음

3. Response time

- MLQ: 우선순위에 따라 다름
- MFQ: interctive한 Process가 높은 우선순위를 갖게 되어 Response time이 짧음

출처: https://jhnyang.tistory.com/156

---

## 페이징과 세그멘테이션

`페이징: 프로세스를 일정 크기인 페이지(page)로 잘라서 메모리에 적재하는 방식`

`세그멘테이션: 논리적으로 독립된 의미의 세그먼트 단위로 동작하는 메모리 관리 비법`

**가상 메모리란?**

`각 프로그램에 실제 메모리 주소가 아닌 가상의 메모리 주소를 주는 방식`

- 멀티태스킹 운영체제에서 흔히 사용되며, 실제 주기억장치(RAM)보다 큰 메모리 영역을 제공하는 방법으로 사용된다.

**가상 메모리를 사용하는 이유?**

`다중 프로그래밍 시스템에 여러 프로세스를 수용하기 위해 주기억장치를 동적 분할하는 메모리 관리 작업이 필요하기 때문`

메모리 관리 기법

1. 연속 메모리 관리(=연속 할당 방식)

   `프로그램 전체가 하나의 커다란 공간에 연속적으로 할당되어야 함`

- 고정 분할 기법: 주기억장치가 고정된 파티션으로 분할(내부 단편화 발생)
  ![내부단편화](https://user-images.githubusercontent.com/55429912/120224636-c7e0d300-c27e-11eb-8d78-12db7b1978d6.jpg)

- 동적 분할 기법: 파티션들이 동적 생성되며 자신의 크기와 같은 파티션에 적재(외부 단편화 발생)
  ![외부단편화](https://user-images.githubusercontent.com/55429912/120224697-e3e47480-c27e-11eb-850e-752dca6888a1.jpg)

2. 불연속 메모리 관리(=불연속 할당 방식)

   `프로그램의 일부가 서로 다른 주소 공간에 할당될 수 있는 기법`

- 페이지: 고정 사이즈의 작은 프로세스 조각(프로세스를 나눈 조각)
- 프레임: 페이지 크기와 같은 주기억장치 메모리 조각(메모리를 나눈 조각)
- 단편화: 기억 장치의 빈 공간 or 자료가 여러 조각으로 나뉘는 현상
- 세그먼트: 서로 다른 크기를 가진 논리적 블록이 연속적 공간에 배치되는 것

**고정 크기**: 페이징(Paging)

**가변 크기**: 세그멘테이션(Segmentation)

- 단순 페이징

  - 각 프로세스는 프레임들과 같은 길이를 가진 균등 페이지로 나뉨
  - 외부 단편화 X
  - 소량의 내부 단편화 존재

- 단순 세그멘테이션

  - 각 프로세스는 여러 세그먼트들로 나뉨
  - 내부 단편화 X, 메모리 사용 효율 개선, 동적 분할을 통한 오버헤드 감소
  - 외부 단편화 존재

- 가상 메모리 페이징

  - 단순 페이징과 비교해 프로세스 페이지 전부를 로드시킬 필요X
  - 필요한 페이지가 있으면 나중에 자동으로 불러들어짐
  - 외부 단편화 X
  - 복잡한 메모리 관리로 오버헤드 발생

- 가상 메모리 세그멘테이션
  - 필요하지 않은 세그먼트들은 로드되지 않음
  - 필요한 세그먼트 있을때 나중에 자동으로 불러들어짐
  - 내부 단편화 X
  - 복잡한 메모리 관리로 오버헤드 발생

**요구 페이징**

- 가상 메모리는 요구 페이징 기법을 통해 **필요한 페이지만 메모리에 적재**하고 사용하지 않는 부분은 그대로 둔다.
- 특정 페이지에 대해 CPU의 요청이 들어온 후에야 해당 페이지를 메모리에 적재하며, 한번도 접근되지 않은 페이지는 물리적 메모리에 적재되지 않는다.
- 이를 통해 메모리 사용량이 감소하고 프로세스 전체를 메모리에 올리는데 들었던 입출력 오버헤드가 감소하며 응답시간이 단축된다.
- 비트를 두어 각 페이지가 메모리에 존재하는지 표시한다.
  - 유효 비트: 페이지가 메모리에 적재됨
  - 무효 비트: 페이지가 현재 메모리에 없거나, 그 페이지가 속한 주소 영역을 프로세스가 사용하지 않는 경우
- CPU가 참조하려는 페이지가 현재 메모리에 올라와 있지 않아 무효비트로 세팅되어 있는 경우를 '페이지 부재'가 일어났다고 한다.

**Page Reference String**란?

![Page refernce String](https://user-images.githubusercontent.com/55429912/120226399-180d6480-c282-11eb-8c43-1e52f622e75f.jpg)

`CPU의 주소 요구에 따라 페이지 결함이 일어나지 않는 부분은 생략하여 표시하는 방법`

**페이지 교체 알고리즘**

필요한 페이지만 메모리에 적재하여도 결국은 메모리는 가득 차게 될것이고, 올라와있던 페이지중 어떤 페이지를 OUT시킬지 정하는 알고리즘
(이때, OUT되는 페이지를 victim page라고 함)

1. FIFO: 메모리에 먼저 올라온 페이지를 먼저 내보내는 알고리즘

- 초기화 코드에 적합

2. OPT(Optimal): 앞으로 가장 사용하지 않을 페이지를 우선적으로 내보내는 알고리즘

- 실질적으로 페이지가 앞으로 잘 사용되지 않을 것이라는 보장이 없기 때문에 수행하기 어려운 알고리즘

3. LRU(Least-Recently-Used): 최근에 사용하지 않은 페이지를 먼저 내보내는 알고리즘

- 과거를 기반으로 판단하므로 실질적으로 사용 가능한 알고리즘
- 교체 방식
  - Global 교체: 메모리 상의 모든 프로세스 페이지에 대해 교체
  - Local 교체: 메모리 상의 자기 프로세스 페이지에서만 교체

---

## 메모리

**메인 메모리란?**

`메인 메모리는 CPU가 직접 접근할 수 있는 접근 장치, 프로세스가 실행되려면 프로그램이 메모리에 올라와야 함`

**MMU(Meomory management unit)란?**

![MMU](https://user-images.githubusercontent.com/55429912/120228354-e39ba780-c285-11eb-8ea9-d6e774f3a7d1.png)

`CPU코어 안에 탑재되어 가상 주소를 실제 메모리 주소로 변환해주는 장치`

메모리의 공간이 한정적이기 때문에 사용자에게 더 많은 메모리를 제공하기 위해 **가상 주소**라는 개념이 등장

**가상주소란?**

`가상 메모리 기법으로 제공되는 주소 공간으로서, 프로세스의 관점에서 사용하는 주소`

**MMU의 메모리 보호**

프로세스는 독립적인 메모리 공간을 가져야하고, 자신의 공간만 접근해야 한다.

따라서 한 프로세스에게 합법적인 주소 영역을 설정하고, 잘못된 접근이 오면 trap(CPU가 자기 자신한테 Interrupt를 거는 것)을 발생시키며 보호한다.

![MMU의 메모리 보호](https://user-images.githubusercontent.com/55429912/120228669-8bb17080-c286-11eb-8a69-9bbe84c20067.png)

- base와 limit 레지스터를 활용한 메모리 보호 기법

  - base 레지스터: 메모리상의 프로세스 시작 주소를 물리 주소로 저장
    - 프로그램이 합법적으로 접근할 수 있는 메모리 상의 가장 작은 주소 즉, 시작 주소를 가지고 있다.
  - limit 레지스터: 프로세스의 사이즈를 저장
    - 프로그램이 기준 레지스터 값부터 접근할 수 있는 메모리의 범위를 보관

  `base <= process < base + limit`

  **범위를 벗어나면 예외 상황이라는 소프트웨어적인 인터럽트 발생**

  사용자 모드인 경우에 기준 레지스터와 한계 레지스터를 사용해서 메모리를 보호

  커널 모드에서는 메모리에 무제한으로 접근이 가능

**메모리 접근 명령은 특권 명령이 아니지만 올바르지 않은 접근 시도로부터 메모리를 보호하기 위해서는 기준 레지스터와 한계 레지스터의 값을 세팅하는 연산은 특권 명령으로 규정해야함**

**메모리 과할당(Over allocating)**

`실제 메모리 사이즈보다 더 큰 사이즈의 메모리를 프로세스에 할당한 상황`

1. 페이지 폴트 발생
2. 페이지 폴트를 발생시킨 페이지 위치를 디스크에서 Search
3. 메모리의 빈 프레임에 페이지를 올려야 하는데, 모든 메모리가 사용중이라 빈 프레임이 없음

**페이지 교체**

`swapping 기법에서 하나의 프로세스를 swap out하여 빈 프레임을 확보하는 것`

1 ~ 3에 해당하는 메모리 과할당 상황 발생 

4. 희생 프레임을 선정하여 디스크에 변경 사항을 기록하고 페이지 테이블을 업데이트 
5. 빈 프레임에 페이지 폴트가 발생한 페이지를 올리고, 페이지 테이블 업데이트

페이지 교체가 이루어지면 아무일이 없던 것처럼 프로세스를 계속 수행시켜줘야함

이때 아무일도 일어나지 않은 것처럼 하려면 페이지 교체 당시 오버헤드를 최대한 줄여야함!!

빈프레임이 없을 경우 `victim 프레임을 비울 때`와 `원하는 페이지를 프레임으로 올릴 때` 두번의 디스크 접근이 이루어짐

오버헤드를 감소 시키는 방법

1. 변경 비트를 모든 페이지마다 설정하여, victim 페이지가 정해지면 해당 페이지의 비트를 확인
   - 변경 bit가 set이면 해당 페이지 내용이 디스크 상의 페이지 내용과 달라졌다는 뜻(페이지가 메모리에 올라온 후 수정이 일어난 것. 즉, 디스크에 기록 해야함)
   - 변경 bit가 clear면 디스크 상의 페이지 내용과 메모리 상의 페이지가 일치한다는 뜻(디스크에 기록할 필요 X)

`변경 Bit를 통해 디스크에 기록하는 횟수를 줄이면서 오버헤드에 대한 수를 감소시키는 방법`

2. 페이지 교체 알고리즘을 상황에 따라 선택
   - 현재 상황에서 페이지 폴트를 발생할 확률을 최대한 줄여줄 수 있는 교체 알고리즘을 선택
     - FIFO, OPT, LRU 등..

---

## 캐시 메모리

`주기억장치에 저장된 내용의 일부를 임시로 저장해두는 기억장치`

**캐시 메모리 사용 이유?**

`CPU(빠름)와 메모리(느림)의 속도 차이로 인한 병목 현상을 완화하기 위해 사용`

**지역성이란?**

`기억 장치 내의 정보를 균일하게 접근 하는 것이 아닌, 한 순간에 특정 부분을 집중적으로 참조하는 특성`

- 시간 지역성: 최근에 참조된 주소의 내용은 곧 다음에도 참조된다는 특성
- 공간 지역성: 실제 프로그램이 참조된 주소와 인접한 주소의 내용이 다시 참조된다는 특성

**캐시 미스**

1. Compulsory Miss(=Cold Miss)
  - 최초 캐시 메모리가 초기화된 상태에서 발생하는 Miss
  - locality를 통해 미리 가져오는 방식으로 해결
2. Capacity Miss
  - 전체적인 용량 부족으로 인한 Miss
  - 용량을 늘려서 해결
3. Conflict Miss
  - Direct나 Set associate Mapping에서 같은 부분을 번갈아 사용하면서 발생하는 Miss
  - 캐시 용량과는 상관 X
  - Fully associate Mapping을 통해 해결

**캐시라인이란?**

`CPU가 메모리로부터 데이터를 가져올 때는 바이트 단위로 가져오지 않고 캐시라인을 가득 채울 만큼의 데이터를 가져오는 것`

**캐시라인을 사용하는 이유?**

- 일반적으로 애플리케이션의 경우 인접한 바이트들을 사용하는 경우가 많기 때문에 CPU의 메모리 접근 횟수를 줄여 성능을 향상 시키기 위함

**캐시 접근**

1. Direct Mapping(직접 사상)
  
  `주기억장치의 블록들이 지정된 한 개의 캐시 라인으로만 사상될 수 있는 매핑 방법`

  ![image](https://user-images.githubusercontent.com/55429912/120374600-b833be00-c354-11eb-9ad1-6ea059215437.png)

  - 간단하고 구현하는 비용이 적게듦
  - 적중률이 낮아질 수 있음
2. Fully Associative Mapping
  
  `비어있는 캐시메모리가 있으면, 마음대로 주소를 저장하는 방식`
  
  - 조건이나 규칙이 없어서 특정 캐시 Set내의 모든 블럭을 한번에 찾아 원하는 데이터가 있는지 검사
  - CAM(Content Addresaable Memory)라는 특수 형태의 메모리 구조를 사용하는데 복잡하고 비용이 높음
3. Set Associative Mapping

  `Direct + Associative를 섞은 방식, 특정 행을 지정해서 그 행안의 어떤 열이든 비어있으면 저장하는 방식`

- Direct에 비해서 검색은 오래 걸리지만 저장이 빠름
- Associative에 비해 저장이 느린 대신 검색이 빠름

---

이와 관련해서 좋은 글

자료구조의 성능을 비교할 때는 원소의 크기, 지역성에 대한 캐시미스 입니다.

vector는 연속적으로 데이터를 저장하기 때문에 지역성이 높아 캐시 효율이 좋습니다.

원시 타입이나 간단한 구조체에 대해서는 vector가 list에 비해 성능이 좋습니다.

반면에 list는 많은 상황에서 캐시 미스가 발생해 크기가 작은 원소에 대해서는 vector에 비해 느립니다.

그러나 원소의 크기가 커지게 되면 vector의 캐시 효율이 떨어지게 되므로 list가 상대적으로 성능이 좋아지게 됩니다.

그리고 어떤 상황에서도 안정적인 성능을 보이는 것은 deque 입니다.

deque는 vector의 단점인 복사와 단편화를 줄인 버전 또는 vector와 list의 중간 정도로 생각할 수 있는데, 원소가 추가될 때 공간이 부족하면 새로운 배열로 원소들을 복사하는 것이 아니라
새로운 메모리 블록을 할당합니다.

이때문에 vector보다는 지역성이 떨어지지만 vector보다 일관된 성능을 가지게 됩니다.

---

[출처] https://cho001.tistory.com/136?category=863667

---

## 파일 시스템(File System)

**파일 시스템이란?**

`컴퓨터에서 파일이나 자료를 쉽게 발견 및 접근할 수 있도록 보관 또는 조직하는 체제`

- 파일 시스템은 일반적으로 크기가 일정한 블록들의 배열에 접근할 수 있는 자료 보관 장치 위에 생성되어 이러한 배열들을 조직함으로 파일이나 디렉토리를 만들며 어느 부분이 파일이고 어느 부분이 공백인지를 구분하기 위하여 각 배열에 표시를 해둔다.

**접근 방법**

1. 순차 접근(Sequential Access)

`가장 간단한 접근 방법으로 대부분 연산은 read, write`

![순차 접근](https://user-images.githubusercontent.com/55429912/120263097-0190f880-c2d6-11eb-9356-1f30d6d717ae.png)

- 현재 위치를 가리키는 포인터에서 시스템 콜이 발생할 경우 포인터를 앞으로 보내면서 read와 write를 진행
- 뒤로 돌아갈 땐 지정한 offset만큼 되감기를 해야한다(테이프 모델 기반)

2. 직접 접근(Direct Access)

`특별한 순서없이, 빠르게 레코드를 read, write 가능`

![직접접근](https://user-images.githubusercontent.com/55429912/120263591-f5f20180-c2d6-11eb-9600-eecebd6eb4e6.png)

- 현재 위치를 가리키는 cp변수만 유지하면 직접 접근 파일을 가지고 순차 파일 기능을 쉽게 구현이 가능
- 무작위 파일 블록에 대한 임의 접근을 허용(순서의 제약이 없음)
- 대규모 정보를 접근할 때 유용(데이터 베이스에 활용)

3. 기타 접근

`직접 접근 파일에 기반하여 색인 구축`

![기타 접근](https://user-images.githubusercontent.com/55429912/120264238-49b11a80-c2d8-11eb-8448-3320422c04fa.png)

- 크기가 큰 파일을 입출력 탐색할 수 있게 도와주는 방법

**디렉터리와 디스크 구조**

- 1단계 디렉터리

  `가장 간단한 구조`

  ![image](https://user-images.githubusercontent.com/55429912/120265093-34d58680-c2da-11eb-8410-d1da3d6ec7cd.png)

  - 파일들은 서로 유일한 이름을 가짐. 서로 다른 사용자라도 같은 이름 사용 불가

- 2단계 디렉터리

  `사용자마다 개별적인 디렉터리`

  ![image](https://user-images.githubusercontent.com/55429912/120265177-64848e80-c2da-11eb-9c81-b8779db723bd.png)

  - MFD(Master File Deirectory): 사용자의 이름과 계정 번호로 색인되어 있는 디렉터리
  - UFD(User File Directory): 자신만의 사용자 파일 디렉터리

- 트리 구조 디렉터리

  `2단계 구조에서 확장된 다단계 트리 구조`

  ![image](https://user-images.githubusercontent.com/55429912/120265329-bfb68100-c2da-11eb-9387-a2625e4636d8.png)

  - 한 비트를 활용하여, 일반 파일(0)인지 디렉터리 파일(1)인지 구분
  - 파일 또는 디렉토리의 공유를 허용하지 않음

- 비순환 그래프 디렉터리(Acyclic Graph Directory)

  `디렉터리들이 서브디렉터리들과 파일들을 공유할 수 있도록 허용하는 구조`

  ![image](https://user-images.githubusercontent.com/55429912/120266555-250b7180-c2dd-11eb-84a3-3f16998d8770.png)

  - 디렉터리들이 서브 디렉터리들과 파일들을 공유할 수 있도록 허용
  - 하나의 파일이나 디렉토리가 여러개의 경로 이름을 가질 수 있다.
  - 링크는 다른 파일이나 서브 디렉터리를 가리키는 포인터를 가지고 참조
  - 공유 파일 삭제 시 존재하지 않는 파일을 가리키는 Dangling 포인터 가능성
    - 참조계수를 사용하여 모든 참조가 지워질 때까지 원본 파일으 보존하여 해결

- 일반 그래프 디렉터리(General Graph Directory)

  `트리 구조에 링크를 더해 순환을 허용하는 그래프 구조`

  ![image](https://user-images.githubusercontent.com/55429912/120267401-d8c13100-c2de-11eb-8eae-fca6d516875e.png)

  - 사이클이 허용
  - 불필요한 파일제거를 위해 참조카운터가 필요
