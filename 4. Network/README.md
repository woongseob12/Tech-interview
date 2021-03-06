# Network

## Index<br>

<ol>
    <li>OSI 7 Layer</li>
    <li>GET & POST</li>
    <li>TCP/ UDP</li>
    <li>TCP 3-way handshake & 4-way hand shake</li>
    <li>HTTP & HTTPS</li>
    <li>ARP Spoofing</li>
</ol>
<br>
<hr>

## OSI 7 Layer

![image](https://user-images.githubusercontent.com/55429912/120319789-5ce5d980-c31c-11eb-8e73-021f9fb224bd.png)

- 프로토콜을 기능별로 나눔
- 각 계층은 하위 계층의 기능만을 이용하고, 상위 계층에게 기능을 제공

<br>
<table border="3">
    <tr>
        <th>계층</th>
        <th>이름</th>
        <th>기능</th>
        <th>단위</th>
        <th>프로토콜</th>
        <th>장비</th>
    </tr>
    <tr>
        <td>7</td>
        <td>응용(Application)</td>
        <td>사용자 인터페이스, 데이터베이스 관리 등의 서비스 제공</td>
        <td>Message, Data</td>
        <td>DNS</td>
        <td>L7 Switch</td>
    </tr>
    <tr>
        <td>6</td>
        <td>표현(Presentaiton))</td>
        <td>파일 인코딩, 암호화, 압축 등 기능을 제공 </td>
        <td></td>
        <td></td>
        <td>L6 Switch</td>
    </tr>
    <tr>
        <td>5</td>
        <td>세션(Session)</td>
        <td>
            <ul>
               <li>데이터 통신을 위한 논리적 연결 담당</li>
               <li>TCP/IP세션을 만들고 없애는 책임을 진다</li>
            </ul>
         </td>
        <td></td>
        <td>API, Socket</td>
        <td>L5 Switch</td>
    </tr>
    <tr>
        <td>4</td>
        <td>전송(Transport)</td>
        <td>
            <ul>
               <li>TCP/ UDP 프로토콜을 통해 통신 활성화</li>
               <li>TCP: 신뢰성, 연결지향적</li>
               <li>UDP: 비신뢰성, 비연결성, 실시간</li>
            </ul>
        </td>
        <td>Segment</td>
        <td>TCP, UDP</td>
        <td>L4 Switch</td>
    </tr>
    <tr>
        <td>3</td>
        <td>네트워크(Network)</td>
        <td>
            <ul>
               <li>데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능</li>
               <li>라우터를 통해 이동할 경로를 선택하여 IP주소를 지정하고, 해당 경로에 따라 패킷을 전달</li>
               <li>라우팅, 흐름제어, 오류제어, 세그먼테이션 등을 수행</li>
            </ul>      
         </td>
        <td>Packet</td>
        <td>IP, ARP</td>
        <td>라우터</td>
    </tr>
    <tr>
        <td>2</td>
        <td>데이터 링크(Data link)</td>
        <td>
            <ul>
               <li>물리 계층으로 송,수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도움</li>
               <li>MAC주소를 이용해 통신</li>
               <li>Frame에 MAC주소를 부요하고 에러검출, 재전송, 흐름 제어를 진행한다</li>
            </ul>
         </td>
        <td>Frame</td>
        <td>MAC, PPP</td>
        <td>브리지, 스위치</td>
    </tr>
    <tr>
        <td>1</td>
        <td>물리(Physical)</td>
        <td>전기적, 기계적, 기능적인 특성을 이용해 데이터 전송</td>
        <td>Bit</td>
        <td>Ethernet RS-232C</td>
        <td>허브, 리피터</td>
    </tr>
</table>
<br>
<hr>

## TCP/UDP

<br>

**Transport 계층에서 사용하는 프로토콜**

### TCP(Transmission Control Protocol)

![image](https://user-images.githubusercontent.com/55429912/120324955-29a64900-c322-11eb-8274-48587566b752.png)

- **신뢰성** 있는 데이터 전송을 지원하는 **연결 지향형** 프로토콜
- 흐름제어, 혼잡제어, 오류제어를 통해 신뢰성을 보장(그러나 이 때문에 UDP보다 전송 속도가 느림)
- 전이중(Full-Duplex), Point-To-Point 방식
- 일반적으로 IP와 함께 사용되며, IP가 데이터의 배달을 처리한다면 TCP는 패킷을 추적 및 관리한다.
  - 데이터를 여러 개의 패킷들로 나누고 패킷 번호를 붙인 후 송신, 수신 측은 각 패킷들을 재조립

**흐름제어(Flow control)란?**

`송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법`

- 수신측이 송신측보다 속도가 빠른 것은 아무 문제가 되지 않음
- 송신측이 수신측보다 속도가 빠르면 제한된 저장용량을 초과하여 이후에 도착하는 데이터의 손실을 유발할 수 있음

흐름 제어 방식

1. Stop & Wait

   ![image](https://user-images.githubusercontent.com/55429912/120322385-50af4b80-c31f-11eb-9bfa-3ac3898f0294.png)

   `매번 전송한 패킷에 대해 확인응답을 받아야만 그 다음 패킷을 전송하는 방법`

2. 슬라이딩 윈도우

   ![image](https://user-images.githubusercontent.com/55429912/120322412-586ef000-c31f-11eb-91d5-9fc8292c93b5.png)

   `수신 측에서 설정한 윈도우 크기만큼 송신측에서 확인 응답 없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하여 제어하는 기법`

   - 송신 버퍼의 범위는 수신 측의 여유 버퍼 공간을 반영하여 동적으로 바뀜

**혼잡제어(Congestion control)란?**

`송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법`

- 한 라우터에 데이터가 몰릴 경우, 라우터는 자신에게 온 데이터를 모두 처리할 수 없어 오버플로우나 데이터 손실 발생

혼잡 제어 방식

1. AIMD(Additive Increase/ Muticative Decrease)

   ![image](https://user-images.githubusercontent.com/55429912/120349614-371afd80-c339-11eb-8e5c-c07848c137a8.png)

   `처음 패킷을 하나씩 보내고 문제없이 도착하면 윈도우 크기(단위 시간 내에 보내는 패킷의 수)를 1씩 증가시켜가며 전송하는 방법. 만일 패킷 전송을 실패하거나 TIME_OUT이 되면 윈도우 크기를 절반으로 줄임`

   장점 :

   - 공평한 방식으로 나중에 진입하는 쪽이 처음에는 불리하지만 시간이 흐르면 평형 상태로 수렴

   단점:

   - 초기에 네트워크의 높은 대역폭을 사용하지 못하여 오랜시간이 걸림
   - 네트워크가 혼잡해지는 상황을 미리 감지하지 못함(네트워크가 혼잡해지고 나서야 대역폭을 줄이는 방식)

2. Slow start

   ![image](https://user-images.githubusercontent.com/55429912/120423796-163cc180-c3a6-11eb-9b05-894c6af82b34.png)

   `윈도우 크기를 2배씩 증가, 혼잡이 감지되면 윈도우 크기를 1로 줄임`

   - 시간이 지날수록 AIMD보다 빠르게 윈도우 크기를 증가시킴
   - 임계점을 사용하여 Slow Start를 제어
     - slow start threshold(ssthresh)
     - 윈도우 크기를 지수적으로 증가시키다 보면 크기가 기하급수적으로 늘어나 제어가 힘들어짐
     - 임계점에 도달하면 선형적으로 1씩 윈도우 크기를 증가

3. Fast Retransmit(빠른 재전송)

   ![image](https://user-images.githubusercontent.com/55429912/120423856-32d8f980-c3a6-11eb-98a8-a6b4b788b1a6.png)

   `수신측에서는 잘 도착한 마지막 패킷의 다음 순번을 ACK패킷에 실어서 보내고, 이런 중복 ACK를 3개 받으면 재전송이 이루어짐`

   - 패킷을 받는 수신자 입장에서는 세그먼트로 분할된 내용들이 순서대로 도착하지 않는 경우가 생길 수 있음
   - 송신 측은 자신이 설정한 타임아웃 시간이 지나지 않아도 바로 해당 패킷을 재전송할 수 있기 때문에 빠른 전송률을 유지할 수 있음
   - 송신측에서 설정한 타임아웃까지 ACK를 받지 못하면 혼잡이 발생한 것으로 판단하여 혼잡 회피를 한다.

4. Fast Recovery(빠른 회복)

   ![image](https://user-images.githubusercontent.com/55429912/120423932-63209800-c3a6-11eb-9274-ef18e1897dac.png)

   `혼잡한 상태가 되면 윈도우 크기를 반으로 줄이고 선형 증가 시키는 방법`

   - 혼잡 상황 후 Slow Start에서 윈도우 크기를 키울 때 너무 오래 걸린다는 단점을 보완한 방식
   - 혼잡 상황 후에는 AIMD방식으로 동작

**오류제어란?**

`오류를 검출하고 정정하는 기능`

- ARQ(Automatic Repeat Request) 기법을 사용해 프레임이 손상되었거나 손실되었을 경우, 재전송을 통해 오류를 복구

1. Stop and Wait ARQ

   - 송신측에서 1개의 프레임을 송신하고, 수신측에서 수신된 프레임의 에러 유무에 따라 ACK/ NAK을 보내는 방식
   - 수신측이 데이터를 받지 못했을 경우, NAK을 보내고 NAK를 받은 송신측은 데이터를 재전송
   - 데이터나 ACK이 분실되었을 경우 일정 간격의 시간을 두고 타임아웃이 발생하면 송신측은 데이터를 재전송

2. Go-Back-n ARQ(슬라이딩 윈도우)

   - 전송된 프레임이 손상되거나 분실된 경우, 확인된 마지막 프레임 이후의 모든 프레임을 재전송
     ![image](https://user-images.githubusercontent.com/55429912/120425976-28206380-c3aa-11eb-8f8f-c7317b2183b0.png)

3. SR(Selective-Reject) ARQ
   - 손상, 손실된 프레임만 재전송(GBn ARQ의 확인된 마지막 프레임 이후의 모든 프레임을 재전송하는 단점을 보완한 기법)
   - 별도의 데이터 재정렬을 수행
   - 수신측에 별도의 버퍼를 두어 받은 데이터의 정렬이 필요

<table>
   <tr>
      <th>GBn(Go-Back-n) ARQ</th>
      <th>SR(Selective-Reject) ARQ</th>
   </tr>
   <tr>
      <td>손상, 손실된 프레임 이후의 모든 프레임을 재전송</td>
      <td>손상, 손실된 프레임만을 재전송</td>
   </tr>
   <tr>
      <td>구조가 비교적 간단하고 구현이 단순</td>
      <td>구조가 복잡(프레임 재배열 등의 추가 로직 필요)</td>
   </tr>
   <tr>
      <td>데이터 폐기 방식을 사용하여 추가적인 버퍼가 필요 없음</td>
      <td>순차적이지 않은 프레임을 재배열하기 위한 버퍼가 필요</td>
   </tr>
   <tr>
      <td>비용이 비교적 저렴</td>
      <td>비용 및 유지관리 비용이 높음</td>
   </tr>
</table>

**TCP Header**

TCP는 상위계층으로부터 데이터를 받아 **헤더**를 추가해 IP로 전송

![image](https://user-images.githubusercontent.com/55429912/120325539-b8b36100-c322-11eb-995c-0b53bfcb99ce.png)

<table border="1">
   <tr>
      <th>필드</th>
      <th>내용</th>
      <th>크기(bit)</th>
   </tr>
   <tr>
      <td>Source Port</td>
      <td>TCP로 연결되는 가상 회선 양단의 송신 프로세스의 포트 주소</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Destination Port</td>
      <td>TCP로 연결되는 가상 회선 양단의 수신 프로세스의 포트 주소</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Sequence Number</td>
      <td>송신자가 지정하는 순서 번호, 전송되는 바이트 수 기준으로 증가</td>
      <td>32</td>
   </tr>
   <tr>
      <td>Acknowledgment Number</td>
      <td>수신 프로세스가 제대로 수신한 바이트의 수 응답 용</td>
      <td>32</td>
   </tr>
   <tr>
      <td>Header Length(Data Offset)</td>
      <td>TCP 헤더 길이를 4Byte 단위로 표시</td>
      <td>4</td>
   </tr>
   <tr>
      <td>Resv(Reserved)</td>
      <td>나중을 위해 0으로 채워진 예약 필드</td>
      <td>6</td>
   </tr>
   <tr>
      <td>Flag Bit</td>
      <td>
         <ul>
            <li>URG: 긴급 위치 필드 유효 여부 설정</li>
            <li>ACK: 응답 유효 여부 설정(정상 수신시 ACK(=SYN + 1)전송)</li>
            <li>PSH: 수신측에 버퍼링된 데이터를 상위 계층에 즉시 전달</li>
            <li>RST: 연결 리셋 응답 혹은 유효하지 않은 세그먼트 응답</li>
            <li>SYN: 연결 설정 요청. 양쪽이 보낸 최초 패킷에만 SYN 플래그 설정</li>
            <li>FIN: 연결 종료 의사 표시</li>
         </ul>
      </td>
      <td>6</td>
   </tr>
   <tr>
      <td>Window Size</td>
      <td>수신 윈도우의 버퍼 크기 지정(0이면 송신 중지)<br> 상대방의 확인 없이 전송가능한 최대 바이트 수</td>
      <td>16</td>
   </tr>
   <tr>
      <td>TCP Checksum</td>
      <td>헤더와 데이터의 에러 확인 용도</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Urgent Pointer(긴급 위치)</td>
      <td>현재 순서 번호부터 표시된 바이트 까지 긴급한 데이터임을 표시<br>
      URG 플래그 비트가 지정된 경우에만 유효</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Options</td>
      <td>추가 옵션 있을 경우 표시</td>
      <td>0 ~ 40</td>
   </tr>
</table>

<br>

### UDP(User Datagram Protocol)

![image](https://user-images.githubusercontent.com/55429912/120325014-332fb100-c322-11eb-8f72-66cdd55743b9.png)

- 비연결형, 신뢰성이 없는 프로토콜
- 데이터를 **데이터그램** 단위로 처리하는 프로토콜
- 데이터 전송의 신속성(실시간 방송, 온라인 게임 등에서 사용)
- 신뢰성보다는 연속성이 중요한 서비스에 사용(RTP(Real-Time Transport Protocol), DNS)
- UDP헤더의 Checksum 필드를 통해 최소한의 오류만 검출

**UDP Header**

![image](https://user-images.githubusercontent.com/55429912/120427071-38394280-c3ac-11eb-80ce-490c1c7abbc8.png)

<table border="1">
   <tr>
      <th>필드</th>
      <th>내용</th>
      <th>크기(bit)</th>
   </tr>
   <tr>
      <td>Source Port</td>
      <td>송신 포트 번호</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Destination Port</td>
      <td>수신 포트 번호</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Length</td>
      <td>헤더와 데이터 포함 전체 길이</td>
      <td>16</td>
   </tr>
   <tr>
      <td>Checksum</td>
      <td>헤더와 데이터의 에러 확인 용도<br>UDP는 에러 복구를 위한 필드가 불필요하기 때문에 TCP 헤더에 비해 간단</td>
      <td>16</td>
   </tr>
</table>

<br>

### Q1) DNS 프로토콜은 UDP일까? TCP일까?

```
A1) UDP
```

### Q2) UDP를 사용하는 이유는?

```
- DNS 요청은 일반적으로 매우 작고, UDP 세그먼트에 적합
- UDP는 신뢰할 순 없지만, Applciation layer에서 Time out, resend을 통해 안정성을 보완할 수 있음
- UDP가 훨씬 빠름(DNS에서 서버의 로드도 중요한 요소이기 때문)
```

### Q3) TCP는 아예 안쓰는가?

```
- 메시지가 512byte를 초과하는 경우, TCP를 통해 질의 응답을 진행
- Zone-Trasnfer, Master-Slaver 구성시 Zone Transfer가 이루어지는데, 이때는 TCP를 사용하여 Zone File을 주고 받음
```

<br>
<hr>

## TCP 3-way handshake & 4-way hand shake

<br>

### TCP 3-way handshake

<br>

TCP는 장치들 사이에 논리적인 접속을 성립(establish)하기 위하여 3-way handshake를 통해 **연결 성립**

<br>

![3-way](https://user-images.githubusercontent.com/55429912/119258039-f7e70100-bc02-11eb-8d63-acd5ecb14afa.png)

1. 클라이언트는 서버에 접속을 요청하는 SYN 패킷을 전송

   `Client: SYN_SENT`

2. 서버는 SYN 요청을 받고, 클라이언트에게 요청을 수락한다는 ACK와 SYN flag가 설정된 패킷을 발송

   `Server: SYN_RECEIVED`

3. 클라이언트는 서버에게 ACK을 보내고 연결이 성립

   `Client: ESTABLISHED`

   `Server: ESTABLISHED`

<br>

### TCP 4-way handshake

<br>

TCP의 신뢰성 보장을 위해 연결해제시에도 4-way handshake를 통해 **연결 해제**

<br>

![4-way](https://user-images.githubusercontent.com/55429912/119258557-25cd4500-bc05-11eb-8254-58535f94fb9a.png)

1. 클라이언트는 서버와의 연결 종료를 위해 서버에 FIN 패킷을 보냄

   `Client: FIN_WAIT1`

2. 서버는 클라이언트로부터 FIN을 받고 ACK을 보냄

   `Server: CLOSE_WAIT`

   `Client: FIN_WAIT2`

3. 서버가 통신이 끝나면(연결을 종료한 준비가 되면), 클라이언트에게 FIN 패킷을 보냄

   `Server: LAST_ACK`

4. 클라이언트는 ACK를 보냄

   `Client: TIME_WAIT`

   `Server: ClOSED`

<br>

<hr>

## HTTP & HTTPS

<br>

### HTTP(HyperText Transfer Protocol)

- 인터넷 상에서 클라이언트와 서버간에 요청/응답으로 정보를 주고 받을 수 있는 프로토콜
- 주로 HTML 문서를 주고받는데 사용
- TCP와 UDP를 사용하며, **80번 포트** 사용
  - 통상적으로 TCP 소켓 사용, 예외적으로 스트리밍 서비스에서는 UDP를 사용하는 경우도 있음
- TCP/IP를 이용하는 응용 프로토콜(applciation protocol)
- HTTP는 연결 상태를 유지하지 않는 비연결성 프로토콜
  - 비연결: 클라이언트가 요청을 서버에 보내고 서버가 적절한 응답을 보내면 바로 연결이 끊김
    ```
    이전 요청과 다음 요청이 연결되어 있지 않다는 의미!!
    하나의 요청/응답 안에서는 연결된 상태로 통신
    HTTP프로토콜이 TCP기반으로 동작: 하나의 요청- 응답
    ```
  - 연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 유지하지 않음
  - 이러한 단점을 해결하기 위해 Cookie와 Session 등장

### HTTPS(HyperText Transfer Protocol Secure)

- HTTP 통신하는 소켓 부분을 인터넷 상에서 정보를 암호화 하는 SSL(Secure Socket Layer)이라는 프로토콜로 대체한 것
- HTTP는 TCP와 통신했지만, HTTPS는 SSL과 통신하고 SSL이 TCP와 통신
- 장점
  - 네트워크 상에서 열람, 수정이 불가능하므로 안전하다.
- 단점
  - 암호화를 하는 과정이 웹 서버에 부하를 준다.
  - HTTPS는 설치 및 인증서를 유지하는데 추가 비용이 발생
  - 인터넷 연결이 끊긴 경우 재인증 시간이 소요
    - HTTP는 비연결형으로 웹 페이지를 보는 중 인터넷 연결이 끊겼다가 다시 연결되어도 페이지를 계속 볼 수 있음
    - HTTPS는 소켓자체에서 인증을 하기 때문에 인터넷 연결이 끊기면 소켓도 끊어져서 다시 HTTPS 인증이 필요

<br>

- HTTP/0.9 - 원-라인 프로토콜
  - 단일 라인으로 구성된 요청
  - 가능한 메서드: GET
  - 단순한 응답
  - 파일 내용 자체로 구성
- HTTP/1.0
  - 1번에 연결에 1번의 Request & 1번의 Response
  - 매번 새로운 연결로 성능 저하
  - 서버 부하 비용 증가
- HTTP/1.1
  - Persistent Connection: 지정한 Timeout 동안 커넥션을 닫지 않는 방식
  - Pipelining: 하나의 커넥션에서 응답을 기다리지 않고 순차적인 여러 요청을 연속적으로 보내 그 순서에 맞춰 응답을 받는 방식으로 지연 시간을 줄이는 방법
  - Head Of Line Blocking
  - Header 구조의 중복
- HTTP/2

  - 기존 HTTP/1.x 버전의 **성능 향상**에 초점을 맞춘 프로토콜
  - HTTP 메시지 전송 방식의 변화
    - 바이너리 프레이밍 계층 사용
    - 파싱, 전송 속도 ↑, 오류 발생 가능성 ↓
  - 요청과 응답의 다중화(Multiplexing)
    - Head Of Line Blocking 해결
  - Stream Prioritization
    - 리소스간 우선 순위 설정 가능
  - Server Push

    ![image](https://user-images.githubusercontent.com/55429912/123412063-1ff3c680-d5ec-11eb-9893-9c9d5adfbe54.png)

  - Header Compression

    ![image](https://user-images.githubusercontent.com/55429912/123411798-d2775980-d5eb-11eb-9a53-3a0e31ccd8b3.png)

    - 헤더의 크기를 줄여 페이지 로드 시간 감소
    <hr>

### 클라이언트와 서버의 통신 흐름 과정

**HTTP**

1. 사용자가 웹 브라우저에 URL 주소 입력
2. DNS 서버에 웹 서버의 호스트 이름을 IP주소로 변경 요청
3. 웹 서버와 TCP 연결 시도
   - 3way-handshaking
4. 클라이언트가 서버에게 데이터 요청
5. 서버가 클라이언트에게 데이터 응답
6. 서버 클라이언트 간 연결 종료
   - 4way-handshaking
7. 웹 브라우저가 웹 문서 출력

**HTTPS**

![image](https://user-images.githubusercontent.com/55429912/120432120-6c186600-c3b4-11eb-81db-ce88aacf245d.png)

1. 클라이언트가 SSL로 암호화된 페이지를 요청
2. 서버는 클라이언트에게 인증서를 전송
   - 인증서에 포함된 내용
     - 서버측 공개키
     - 공개키 암호화 방법
     - 인증서를 사용한 웹서버의 URL
     - 인증서를 발행한 기관 이름
3. 클라이언트는 인증서가 신용있는 cA로부터 서명된 것인지 판단
4. 클라이언트는 CA의 공개키를 이용해 인증서를 복호화하고, 서버의 공개키를 획득
5. 클라이언트는 서버의 공개키를 사용해 랜덤 대칭 암호화키, 데이터 등을 암호화하여 서버로 전송
6. 서버는 자신의 개인키를 이용해 복호화하고 랜덤 대칭 암호화키, 데이터 등을 획득
7. 서버는 랜덤 대칭 암호화키로 클라이언트 요청에 대한 응답을 암호화하여 전송
8. 클라이언트는 랜덤 대칭 암호화키를 이용해 복호화하고 데이터를 이용

---

## 대칭키 & 공개키

**대칭키(Symmetric Key)**

![image](https://user-images.githubusercontent.com/55429912/120472340-bc0d2200-c3e0-11eb-8005-e00189af4b33.png)

`암호화와 복호화에 같은 암호키를 사용하는 알고리즘`

- 동일한 키를 주고 받기 때문에 매우 빠름
- 대칭키 전달과정에서 해킹 위험에 노출될 수 있음

**공개키(Public Key)**

![image](https://user-images.githubusercontent.com/55429912/120472372-c7f8e400-c3e0-11eb-9359-0486ad6d5a71.png)

`암호화와 복호화에 사용하는 암호키를 분리한 알고리즘`

- 자신이 가지고 있는 고유한 암호키(비밀키)로만 복호화할 수 있는 암호키(공개키)를 대중에 공개함

**공개키 암호화 방식 진행 과정**

1. A가 웹 상에 공개된 'B의 공개키'를 이용해 평문을 암호화하여 B에게 보냄
2. B는 자신의 비밀키로 복호화한 평문을 확인, A의 공개키로 응답을 암호화하여 A에게 보냄
3. A는 자신의 비밀키로 암호화된 응답문을 복호화함

**대칭키의 단점을 완벽하게 해결했지만, 암호화 복호화가 매우 복잡함(암호화하는 키와 복호화하는 키가 서로 다르기 때문**

**대칭키와 공개키 암호화 방식을 혼합한다면?**

`SSL 탄생의 시초`

1. A가 B의 공개키로 암호화 통신에 사용할 대칭키를 암호화하고 B에게 보냄
2. B는 암호문을 받고, 자신의 비밀키로 복호화함
3. B는 A로부터 얻은 대칭키로 A에게 보낼 평문을 암호화하여 A에게 보냄
4. A는 자신의 대칭키로 암호문을 복호화함
5. 앞으로 이 대칭키로 암호화를 통신함

**즉, 대칭키를 주고받을 때만 공개키 암호화 방식을 사용하고 이후에는 계속 대칭키 암호화 방식으로 통신하는 것이다**

---

## GET & POST

<br>

### GET:

- 클라이언트에서 서버로 어떠한 리소스에서 **데이터를 요청**하기 위해 사용되는 메서드
- GET을 통한 요청은 URL주소 끝에 파라미터로 포함되어 전송되며, 이 부분을 쿼리 스트링(query string)이라 부름

```
www.example.com/show?name1=value1&name2=value2
```

- 요청의 길이 제한이 있으며, 보안에 취약함(URL에 파라미터가 노출되기 때문에)
- 요청 정보가 여러 개일 경우에는 '&'로 구분
- GET방식은 캐싱을 사용할 수 있어, GET 요청과 그에 대한 응답이 브라우저에 의해 캐시된다.

### POST:

- 클라이언트에서 서버로 리소스를 생성하거나 업데이트하기 위해 **데이터를 변경할 때** 사용되는 메서드
- HTTP Request Message의 Body 부분에 데이터를 담아서 서버로 보냄
- 길이 제한이 따로 없어서 용량이 큰 데이터를 보거나, 보안이 필요할 때 사용(데이터를 암호화하지 않으면 Body의 데이터도 볼 수는 있음)

### 주요 차이점: GET은 HTTP Message에 Body가 없고, POST는 HTTP Message에 Body가 존재!!

<br>
<hr>

## Cookie & Session

- HTTP 프로토콜은 비연결, 상태정보를 유지하지 않으므로 모든 요청 간 의존관계가 없다.
- 즉, 현재 접속한 사용자가 이전에 접속했던 사용자와 같은 사용자인지 아닌지 알수 있는 방법이 없다.
- 연결을 유지하지 않기 때문에 자원 낭비가 줄어드는 것은 큰 장점이지만, 통신마다 새로 연결하기 때문에 클라이언트는 매 요청마다 인증을해야하는 단점이 존재한다.
- HTTP 프로토콜에서 상태를 유지하기 위한 기술로 Cookie와 Session이 있다.

### 쿠키(Cookie)란?

`클라이언트 로컬에 저장되는 키와 값이 들어있는 파일`

- 서버가 HTTP 응답 헤더의 `Set-Cookie`에 내용을 넣어 전달하면, 브라우저는 이 내용을 자체적으로 브라우저에 저장
- 브라우저는 서버에 접속할 때마다 쿠키의 내용을 요청헤더에 넣어서 함께 전달
- 이름, 값, 유효 시간, 경로 등을 포함하고 있음
- 클라이언트의 상태 정보를 브라우저에 저장하여 참조

- 구성 요소
  - 쿠키의 이름(name)
  - 쿠키의 값(value)
  - 쿠키의 만료시간(Expires)
  - 쿠키를 전송할 도메인 이름(Domain)
  - 쿠키를 전송할 경로(Path)
  - 보안 연결 여부(Secure)
  - httpOnly 여부(httpOnly)
  - httpOnly 옵션이 설정된 쿠키는 document.cookie로 쿠키 정보를 읽을 수 없음(쿠키 보호 가능)

**동작 방식**

![image](https://user-images.githubusercontent.com/55429912/120448562-a559d180-c3c6-11eb-98b4-abdada97f602.png)

1. 클라이언트가 서버에 요청
2. 상태를 유지하고 싶은 값을 쿠키로 생성후 응답할때 HTTP 헤더에 쿠키를 포함해서 전송
   ```java
   Set-Cookie: id=id
   ```
3. 전달받은 쿠키는 웹브라우저에서 관리하고 있다가, 다음 요청때 쿠키를 HTTP헤더에 넣어서 전송
   ```java
   cookie: id=id
   ```
4. 서버에서는 쿠키 정보를 읽어 이전 상태 정보를 확인한 후 응답

### 세션(Session)이란?

`클라이언트와 웹서버 간 네트워크 연결이 지속 유지되고 있는 상태`

1. 클라이언트가 서버에 접속시 세션ID를 발급 받음
2. 클라이언트는 세션ID에 대해 쿠키를 사용해서 저장
3. 클라이언트는 서버에 요청할 때, 쿠키의 세션 ID를 서버에 전달해서 사용
4. 서버는 세션 ID를 전달 받아 별다른 작업없이 세션 ID로 세션에 있는 클라이언트 정보를 가져옴
5. 클라이언트 정보를 가지고 서버 요청을 처리하여 클라이언트에게 응답

**세션도 쿠키를 사용하여 값을 주고 받으며 클라이언트의 상태 정보를 유지한다. 즉, 상태 정보를 유지하는 수단은 쿠키이다**

**쿠키와 세션의 차이점**

- 저장 위치
  - 쿠키: 클라이언트(서버 자원 사용 X)
  - 세션: 서버(서버 메모리로 로딩되기 떄문에 세션이 생길 때마다 리소스를 차지)
- 보안
  - 쿠키: 클라이언트에 저장되므로 보안에 취약
  - 세션: 쿠키를 이용해 Session ID만 저장하고 이 값으로 구분해서 서버에서 처리하므로 비교적 보안성이 좋음
- 라이프 사이클
  - 쿠키: 만료시간에 따라 브라우저를 종료해도 계속해서 남아 있을 수 있음
  - 세션: 만료시간을 정할 수 있지만 브라우저가 종료되면 만료시간에 상관없이 삭제된다.
- 속도
  - 쿠키: 클라이언트에 저장되어서 서버에 요청시 빠름
  - 세션: 실제 저장된 정보가 서버에 있으므로 서버의 처리가 필요해 쿠키보다 느리다.
- 용량 제한
  - 쿠키: 한 도메인당 20개, 하나의 쿠키당 4KB로 제한
  - 세션: 개수나 용량의 제한이 없음

---

## REST & RESTful 이란?

### REST(Representational State Transfer)란?

`웹에 존재하는 모든 자원(이미지, 동영상, DB 자원 등)에 고유한 URI를 부여해 활용하는 것`

**특징**

- 웹의 장점을 최대한 활용할 수 있는 클라이언트와 서버간 통신 방식 중 하나
- HTTP URI을 통해 자원을 명시하고, HTTP Method(GET, POST, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것

  - 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고, HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
  - 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여

**구성 요소**

1. 자원(Resource): URI
   - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재
   - 자원을 구별하는 ID는 '/groups/:group_id'와 같은 **HTTP URI**이다.
   - Client는 URI를 이용하여 자원을 지정, 해당 자원의 상태에 대한 조작을 Server에 요청
2. 행위(Verb): HTTP Method
   - HTTP 프로토콜의 Method를 사용한다
     - GET, POST, PUT, DELETE
3. 표현(Representation of Resource)
   - Client가 자원의 상태에 대한 조작을 요청하면 Server는 이에 적절한 응답을 보냄
   - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태로 나타내어 질 수 있음
   - JSON, XML을 통해 데이터를 주고 받는 것이 일반적

- 장점

  - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능
  - 서버와 클라이언트의 역할을 명확하게 분리
  - HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없음

- 단점
  - 표준이 없음
  - 사용할 수 있는 메소드가 4가지 뿐임(HTTP Method 형태가 제한적)

<br>

### REST API란?

![image](https://user-images.githubusercontent.com/55429912/120452596-451a5e00-c3cd-11eb-9eb7-a98902709588.png)

`REST 기반으로 서비스 API를 구현한 것`

API(Application Programming Interface): 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능하도록 하는 것

**특징**

- 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 함
- HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있음

<br>

### RESTful이란?

![image](https://user-images.githubusercontent.com/55429912/120452295-1308fc00-c3cd-11eb-9c89-dd106d121a4c.png)

`REST 형식을 따른 시스템`

**목적**

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것

**RESTful 하지 못한 경우?**

1. CRUD 기능을 모두 POST로만 처리하는 API
2. route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)

---

## Load Balancing(로드 밸런싱)

![image](https://user-images.githubusercontent.com/55429912/120454916-477db780-c3cf-11eb-9243-1aa724dd1d9f.png)

`둘 이상의 CPU or 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것`

Scale-up: 하드웨어의 성능을 올림

Scale-out: 여러대의 서버가 나눠서 일하도록 함

로드 밸런싱: 여러 서버에게 균등하게 트래픽을 분산시켜주는 것

**로드 벨런서 주요 기능**

- NAT(Network Address Translation)

  - 사설 IP주소를 공인 IP주소로 바꾸는데 사용하는 통신망의 주소 변조기

- Tunneling

  - 인터넷상에서 눈에 보이지 않는 통로를 만들어 통신할 수 있게하는 개념
  - 데이터를 캡슐화해서 연결된 상호 간에만 캡슌화된 패킷을 구별해 캡슐화를 해제할 수 있음

- DSR(Dynamaic Source Routing Protocol)
  ![image](https://user-images.githubusercontent.com/55429912/120455945-24073c80-c3d0-11eb-93a0-5714ce78584e.png)

  - 로드 벨런서 사용 시 서버에서 클라이언트로 되돌아가는 경우 목적지 주소를 스위치 IP주소가 아닌 클라이언트의 IP주소로 전달하여 네트워크 스위치를 거치지 않고 바로 클라이언트를 찾아가는 개념

**로드 벨런서 종류**

- L2: MAC주소를 바탕으로 Load Balancing
- L3: IP주소를 바탕으로 Load Balancing
- L4:
  ![image](https://user-images.githubusercontent.com/55429912/120456649-c6272480-c3d0-11eb-954b-2e9de41fe60a.png)
  - Transport Layer에서 Load Balancing
  - TCP, UDP
- L7:
  ![image](https://user-images.githubusercontent.com/55429912/120456817-ebb42e00-c3d0-11eb-9edc-cedfc8dc88e0.png)
  - Application Layer에서 Load Balancing
  - HTTP, HTTPS, FTP

**로드 벨런서가 서버를 선택하는 방식**

1. Round Robin: CPU 스케줄링의 라운드 로빈 방식 활용
2. Least Connections: 연결 개수가 가장 적은 서버 선택(트래픽으로 인해 세션이 길어지는 경우 권장)
3. Source: 사용자 IP를 해싱하여 분배(특정 사용자가 항상 같은 서버로 연결되는 것 보장)

**로드 밸런서 장애 대비**

![image](https://user-images.githubusercontent.com/55429912/120457067-2027ea00-c3d1-11eb-9fb8-785cdc2ef082.png)

`Load Balancer를 이중화하여 장애를 대비`

1. 이중화된 Load Balancer들은 서로 Health Check
   - Active
   - Passive
2. Main Load Balancer가 동작하지 않으면 가상IP는 여분의 Load Balancer로 변경
3. 여분의 Load Balancer로 운영

---

## Blocking I/O & Non-Blocking I/O

**Blocking Model**

![image](https://user-images.githubusercontent.com/55429912/120461591-17d1ae00-c3d5-11eb-97a6-28ed98958dd5.png)

`I/O 작업이 진행되는 동안 유저 프로세스는 자신의 작업을 중단한 채 대기하는 방식`

1. 유저는 커널에게 system call을 통해 작업을 요청
2. 커널에서 데이터가 입력될 때 까지 대기
3. 커널에서 유저에게 데이터를 전달 후 유저 작업을 시작할 수 있음

**유저프로세스는 block 되어 다른 작업을 수행하지 못하고 대기하게 되므로 자원이 낭비됨**

**Non-Blocking Model**

![image](https://user-images.githubusercontent.com/55429912/120462110-92023280-c3d5-11eb-9137-db240089eba3.png)

`I/O 작업이 진행되는 동안 유저 프로세스의 작업을 중단시키지 않는 방식`

1. 유저가 커널에게 작업을 요청
2. 데이터가 입력여부에 상관없이 요청하는 순간 바로 결과가 반환됨
   - 입력 데이터가 없으면 입력 데이터가 없다는 결과 메시지(EWOULDBLOCK)를 반환
3. 입력 데이터가 있을 때까지 1 ~ 2번을 반복
   - 2번에서 결과 메시지를 받은 유저는 다른 작업 진행 가능
4. 입력 데이터가 있으면 유저에게(커널 → 유저) 결과가 전달

**I/O의 진행시간과 관계가 없기 때문에(대기X) 어플리케이션에서 작업을 오랜시간 중지하지 않고도 I/O 작업을 진행할 수 있음**
**그러나 반복적인 system call이 발생하기 때문에 이 경우 또한 자원이 낭비됨**

---

## DNS

**IP주소**

`컴퓨터 네트워크에서 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 특수한 번호`

- IPv4(32bit)로 구성되어 있으며, 127.0.0.1 같은 주소를 말함
- 주소 공간의 부족으로 IPv6(128bit)가 탄생함

**도메인 네임(Domain Name)**

`IP주소를 문자로 표현한 주소`

- 도메인 이름은 사람의 편의성을 위해 만든 주소이므로 사용시 컴퓨터가 이해할 수 있는 IP주소로 변환하는 작업이 필요
- 도메인 네임과 함께 해당하는 IP 주소값을 한 쌍으로 저장하고 있는 데이터베이스를 DNS(Domain Name System)이라고 부름
- 도메인 네임으로 입력하면 DNS를 이용해 컴퓨터는 IP 주소를 받아 찾아갈 수 있음

**작동 방식**

![image](https://user-images.githubusercontent.com/55429912/120473141-ac420d80-c3e1-11eb-9fba-289ef97c51b1.png)

### DHCP & ARP

**DHCP(Dynamic Host Configuration Protocol)란?**

`호스트의 IP 주소 및 TCP/IP 설정을 클라이언트에 자동으로 제공하는 프로토콜`

![image](https://user-images.githubusercontent.com/55429912/120500105-8e81a200-c3fb-11eb-8f41-3b602a36c058.png)

1. 사용자의 PC는 DHCP 서버에서 사용자 자신의 IP주소, 가장 가까운 라우터의 IP주소, 가장 가까운 DNS서버의 IP주소를 받는다.
2. ARP 프로토콜을 이용하여 IP주소를 기반으로 가장 가까운 라우터의 MAC주소를 알아낸다.

- MAC(Media Access Control) 주소: 네트워크 카드 하드웨어에 부여된 고유한 물리적 주소

3. 2의 과정을 통해 외부와 통신할 준비를 마친 뒤, DNS Query를 DNS 서버에 송신한다. DNS 서버는 이에대한 결과로 웹 서버의 IP주소를 사용자 PC에게 돌려준다.
4. HTTP Request를 위해 TCP 소켓을 개방하고 연결한다.(이 과정에서 3-way-handshaking 발생)
5. 이에 대한 응답으로 웹페이지의 정보가 사용자의 PC로 들어온다.

---

## CORS

**CORS(Cross-Origin Resource Sharing)란?**

`서로 다른 Origin(도메인 혹은 포트가 다른 것)에서 리소스를 공유 할 수 있도록 하는 정책`

- 브라우저는 SOP에 의해 서로 다른 Origin에서의 자원 공유를 제한
  - SOP(Same-Origin Policy): 웹 브라우저 보안을 위해 프로토콜, 호스트, 포트가 동일한 서버로만 AJAX요청을 주고 받을 수 있도록 한 정책
- CORS를 통해 CORS정책에 부합하는 요청은 허용하는 것

**CORS 설정방법**

- 서버에서 특정 도메인에서의 요청을 허용
  - API의 응답 헤더에 "Access-Control-Allow-Origin" 값을 넣어줌으로써 CORS 정책을 따르도록 할 수 있음.
  - API에 대해 개별적으로 적용되는 사항이기 때문에, 모든 API에 일일이 대응해주어야 함
  ```javascript
  app.use((req. res, next) => {
     res.header("Access-Control-Allow-Origin","*");   // 모든 도메인
     res.header("Access-Control-Allow-Origin","https://www.naver.com/");   // 특정 도메인
  });
  ```
- Node.js Express 미들웨어 CORS
  - CORS라이브러리를 Express 서버에 설치해서 사용
  ```javascript
   npm i cors --save
  ```

---
