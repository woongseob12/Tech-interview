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
        <td>서비스 제공</td>
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
        <td>데이터 통신을 위한 논리적 연결 담당</td>
        <td></td>
        <td></td>
        <td>L5 Switch</td>
    </tr>
    <tr>
        <td>4</td>
        <td>전송(Transport)</td>
        <td>TCP/ UDP 프로토콜을 통해 통신 활성화</td>
        <td>Segment</td>
        <td>TCP, UDP</td>
        <td>L4 Switch</td>
    </tr>
    <tr>
        <td>3</td>
        <td>네트워크(Network)</td>
        <td>데이터를 목적지까지 가장 안전하고 빠르게 전달(라우팅)</td>
        <td>Packet</td>
        <td>IP, ARP</td>
        <td>라우터</td>
    </tr>
    <tr>
        <td>2</td>
        <td>데이터 링크(Data link)</td>
        <td>물리 계층으로 송수신되는 정보를 관리, Mac주소를 통해 통신</td>
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

## GET & POST

<br>

### GET:

- 클라이언트에서 서버로 어떠한 리소스에서 **데이터를 요청**하기 위해 사용되는 메서드
- GET을 통한 요청은 URL주소 끝에 파라미터로 포함되어 전송되며, 이 부분을 쿼리 스트링(query string)이라 부름

```
www.example.com/show?name1=value1&name2=value2
```

- 요청의 길이 제한이 있으며, 보안에 취약함(URL에 파라미터가 노출되기 때문에)

### POST:

- 클라이언트에서 서버로 리소스를 생성하거나 업데이트하기 위해 **데이터를 보낼 때** 사용되는 메서드
- HTTP Request Message의 Body 부분에 데이터를 담아서 서버로 보냄
- 길이 제한이 따로 없어서 용량이 큰 데이터를 보거나, 보안이 필요할 때 사용(데이터를 암호화하지 않으면 Body의 데이터도 볼 수는 있음)

### 주요 차이점: GET은 HTTP Message에 Body가 없고, POST는 HTTP Message에 Body가 존재!!

<br>
<hr>

## TCP/UDP

<br>

**Transport 계층에서 사용하는 프로토콜**

### TCP(Transmission Control Protocol)

![image](https://user-images.githubusercontent.com/55429912/120324955-29a64900-c322-11eb-8274-48587566b752.png)

- 서버와 클라이언트간에 데이터를 **신뢰성** 있게 전달하기 위해 만들어진 프로토콜
- 데이터를 전송하기 전에 데이터 전송을 위한 연결을 만드는 **연결지향** 프로토콜
- 흐름제어, 혼잡제어
- 전이중(Full-Duplex), Point-To-Point 방식
- IP와 함께 사용되며, IP가 데이터의 배달을 처리한다면 TCP는 패킷을 추적 및 관리한다.

**흐름제어(Flow control)란?**

`송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법`

- 수신측이 송신측보다 속도가 빠른 것은 아무 문제가 되지 않음
- 송신측이 수신측보다 속도가 빠르면 제한된 저장용량을 초과하여 이후에 도착하는 데이터의 손실을 유발할 수 있음

흐름 제어 방식

1. Stop & Wait: 매번 전송한 패킷에 대해 확인응답을 받아야만 그 다음 패킷을 전송하는 방법

   ![image](https://user-images.githubusercontent.com/55429912/120322385-50af4b80-c31f-11eb-9bfa-3ac3898f0294.png)

2. 슬라이딩 윈도우: <u>수신 측에서 설정한 윈도우 크기만큼 송신측에서 확인 응답 없이 세그먼트를 전송</u>할 수 있게 하여 데이터 흐름을 동적으로 조절하여 제어하는 기법

   - 송신 버퍼의 범위는 수신 측의 여유 버퍼 공간을 반영하여 동적으로 바뀜

   ![image](https://user-images.githubusercontent.com/55429912/120322412-586ef000-c31f-11eb-91d5-9fc8292c93b5.png)

**혼잡제어(Congestion control)란?**

`송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법`

- 한 라우터에 데이터가 몰릴 경우, 라우터는 자신에게 온 데이터를 모두 처리할 수 없어 오버플로우나 데이터 손실 발생

혼잡 제어 방식

1. AIMD(Additive Increase/ Muticative Decrease)

   `처음 패킷을 하나씩 보내고 문제없이 도착하면 윈도우 크기(단위 시간 내에 보내는 패킷의 수)를 1씩 증가시켜가며 전송하는 방법. 만일 패킷 전송을 실패하거나 일정 시간이 넘으면 패킷을 보내는 속도를 절반으로 줄임`

   장점 :

   - 공평한 방식으로 나중에 진입하는 쪽이 처음에는 불리하지만 시간이 흐르면 평형 상태로 수렴

   단점:

   - 초기에 네트워크의 높은 대역폭을 사용하지 못하여 오랜시간이 걸림
   - 네트워크가 혼잡해지는 상황을 미리 감지하지 못함(네트워크가 혼잡해지고 나서야 대역폭을 줄이는 방식)

2. Slow start
   `윈도우 크기를 2배씩 증가, 혼잡이 감지되면 윈도우 크기를 1로 줄임`

   - 시간이 지날수록 AIMD보다 빠르게 윈도우 크기를 증가시킴
   - 임계점을 사용하여 Slow Start를 제어
     - slow start threshold(ssthresh)
     - 윈도우 크기를 지수적으로 증가시키다 보면 크기가 기하급수적으로 늘어나 제어가 힘들어짐
     - 임계점에 도달하면 선형적으로 1씩 윈도우 크기를 증가

3. Fast Retransmit(빠른 재전송)

   `수신측에서는 잘 도착한 마지막 패킷의 다음 순번을 ACK패킷에 실어서 보내고, 이런 중복 ACK를 3개 받으면 재전송이 이루어짐`

   - 패킷을 받는 수신자 입장에서는 세그먼트로 분할된 내용들이 순서대로 도착하지 않는 경우가 생길 수 있음
   - 송신 측은 자신이 설정한 타임아웃 시간이 지나지 않아도 바로 해당 패킷을 재전송할 수 있기 때문에 빠른 전송률을 유지할 수 있음
   - 송신측에서 설정한 타임아웃까지 ACK를 받지 못하면 혼잡이 발생한 것으로 판단하여 혼잡 회피를 한다.

4. Fast Recovery(빠른 회복)
   `혼잡한 상태가 되면 윈도우 크기를 반으로 줄이고 선형 증가 시키는 방법`

   -혼잡 상황 후에는 AIMD방식으로 동작

**TCP Header**

TCP는 상위계층으로부터 데이터를 받아 **헤더**를 추가해 IP로 전송

![image](https://user-images.githubusercontent.com/55429912/120325539-b8b36100-c322-11eb-995c-0b53bfcb99ce.png)

<br>

### UDP(User Datagram Protocol)

![image](https://user-images.githubusercontent.com/55429912/120325014-332fb100-c322-11eb-8f72-66cdd55743b9.png)

- 비연결형, 신뢰성이 없는 프로토콜
- 데이터 전송의 신속성(실시간 방송, 온라인 게임 등에서 사용)
- 신뢰성보다는 연속성이 중요한 서비스에 사용
- UDP헤더의 Checksum 필드를 통해 최소한의 오류만 검출

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

- 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약
- 텍스트 교환
- TCP/IP를 이용하는 응용 프로토콜(applciation protocol)
- HTTP는 연결 상태를 유지하지 않는 비연결성 프로토콜(이러한 단점을 해결하기 위해 Cookie와 Session 등장)

### HTTPS(HyperText Transfer Protocol Secure)

- 인터넷 상에서 정보를 암호화하는 SSL 프로토콜을 사용해 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약
- 텍스트를 암호화(공개키 암호화 방식)

<br>
<hr>

## ARP Spoofing

LAN에서 ARP를 이용하여 상대방의 데이터 패킷을 중간에서 가로채는 기법

`ARP(Address Resolution Protocol): IP주소를 MAC주소로 변환해주는 프로토콜`

![ARP spoofing](https://user-images.githubusercontent.com/55429912/119259472-7181ed80-bc09-11eb-981f-984831af3d44.png)

ARP 통신방법:

1. ARP는 기본적으로 MAC 주소를 얻기 위해 IP를 BroadCast방식으로 전송
2. 그 중에 필요한 MAC주소를 가지고 있는 특정 장치의 Response를 이용해 MAC 주소를 얻어냄
3. 받은 MAC 주소를 캐싱 테이블에 저장한 뒤, 이 주소를 이용하여 통신

**ARP Spoofing은 Broadcast로 전송된 IP요청을 받은 후 요청자에게 잘못된 MAC주소를 알려줌. 그리고 올바른 MAC주소를 가진 타겟 장치에 또한 요청자 MAC주소가 아닌 잘못된 MAC주소를 보내줌.**
