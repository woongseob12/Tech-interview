# Computer Arhitecture

## 컴퓨터의 구성

**하드웨어**

![image](https://user-images.githubusercontent.com/55429912/120900328-37840300-c66f-11eb-9eca-6ef75979598c.png)

`컴퓨터를 구성하는 기계적 장치`

1. 중앙처리 장치(CPU)
  - `주기억장치에서 프로그램 명령어와 데이터를 읽어와 처리하고 명령어의 수행 순서를 제어함`
    - 산술논리연산장치(ALU): 비교와 연산을 담당
    - 제어장치: 명령어의 해석과 실행을 담당
    - 레지스터: 속도가 빠른 데이터 기억장소
2. 기억 장치
  - `프로그램, 데이터, 연산의 중간 결과 등을 저장하는 장치`
    - 주기억 장치
      - ROM(Read-only Memory): 비휘발성 메모리, 기억된 내용을 읽은 수는 있지만 바꿀수는 없음
      - RAM(Random-access Memory): 휘발성 메모리, 연산결과를 저장하거나 다음 연산에 상용하는 등 상황에 따라 편리하게 사용할 수 있는 범용 메모리
    - 보조 기억 장치 
      - 비휘발성
      - CPU와 직접적인 데이터 교환X
3. 입출력 장치
  
**소프트웨어**

- 시스템 소프트웨어
  - 운영체제, 컴파일러 
- 응용 소프트웨어
  - 워드 프로세서, 스프레드시트

--- 

## 시스템 버스

![image](https://user-images.githubusercontent.com/55429912/120900779-c8f47480-c671-11eb-8dff-3755d388adaa.png)

`컴퓨터의 구성요소를 서로 연결하고 데이터 전달을 위한 통로`

1. 데이터 버스(Data Bus)
  - `중앙처리장치와 기타 장치 사이에서 데이터를 전달하는 통로`
    - 기억장치, 입출력장치의 명령어와 데이터를 중앙 처리장치로 보내거나, 중앙처리장치의 연산 결과를 기억장치, 입출력장치로 보내는 **양방향버스**
2. 주소 버스(Address Bus)
   - `메모리의 주소를 전달하는 통로`
     - 중앙처리장치가 주기억장치나 입출력장치로 기억장치 주소를 전달하는 **단방향버스**
3. 제어 버스(Control Bus)
   - `중앙처리장치가 기억장치나 입출력장치에 제어 신호를 전달하는 통로`
     - 읽기 동작과 쓰기 동작을 모두 수행하는 **양방향버스**

컴퓨터는 기본적으로 읽고 처리한 뒤 저장하는 과정으로 이루어짐
(READ → PROCESS → WRITE)

CPU는 RAM으로부터 데이터를 읽어 올때 한번에 운영체제의 bit 크기만큼 읽어옴
bit 크기는 **명령을 한번에 처리할 수 있는 레지스터의 비트 크기**
word: 레지스터에 옮겨 놓을 수 있는 데이터 단위
- 32bit 컴퓨터 CPU의 레지스터 처리값: 32bit
- 64bit 컴퓨터 CPU의 레지스터 처리값: 64bit

## 레지스터

`특정한 목적에 사용되는 일시적인 기억장치, 데이터를 읽고 쓰는 기능이 매우 빠르며, 중앙 처리 장치(CPU) 내부에 사용됨`

**종류**

1. 범용 레지스터(General Purpose Register)
2. 특수 레지스터
  - 특별한 용도로 사용하는 레지스터
    - MAR(메모리 주소 레지스터): 읽기와 쓰기 연산을 수행할 주기억장치 주소 저장
    - PC(프로그램 카운터): 다음 수행할 명령어 주소 저장
    - IR(명령어 레지스터): 현재 실행중인 명령어 저장
    - MBR(메모리 버퍼 레지스터): 주기억장치에서 읽어온 데이터 or 저장할 데이터 임시 저장
    - AC(누산기): 연산 결과 임시 저장

**CPU의 동작 과정**

1. 주기억장치는 입력장치에서 입력받은 데이터 또는 보조기억장치에 저장된 프로그램 읽어옴
2. CPU는 프로그램을 실행하기 위해 주기억장치에 저장된 프로그램 명령어와 데이터를 읽어와 처리하고 결과를 다시 주기억장치에 저장
3. 주기억장치는 처리 결과를 보조기억장치에 저장하거나 출력장치로 보냄
4. 제어장치는 1 ~ 3번 과정에서 명령어가 순서대로 실행되도록 각 장치를 제어

**CPU의 명령어 싸이클**

![image](https://user-images.githubusercontent.com/55429912/120902197-df063300-c679-11eb-9fc2-79b23b2f285a.png)

`한 개의 명령어가 CPU에서 수행되는데 필요한 전체 수행 과정`

- 인출(Fetch)
  - 기억장치에 있는 명령어를 인출하는 과정
- 실행(Execute)
  - 명령어를 실행하는 단계로 IR레지스터에 실린 명령어를 해독하고, 해독한 명령어에 따라 필요한 연산이 수행되는 과정
- 간접(Indirect)
  - 간접주소지정방식을 사용하는 명령어에서 Operand 부분의 유효 주소를 결정하는 과정
- 인터럽트(Interrupt)
  - CPU가 현재 처리 중인 프로그램 루틴을 중단시키고 다른 동작을 수행하도록 하는 과정 