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

### TCP(Transmission Control Protocol)

- 서버와 클라이언트간에 데이터를 **신뢰성** 있게 전달하기 위해 만들어진 프로토콜
- 데이터를 전송하기 전에 데이터 전송을 위한 연결을 만드는 **연결지향** 프로토콜
- 흐름제어, 혼잡제어

  - 흐름제어: 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법
  - 혼잡제어: 송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법

- 전이중(Full-Duplex), Point-To-Point 방식

<br>

### UDP(User Datagram Protocol)

- 비연결형, 신뢰성이 없는 프로토콜
- 데이터 전송의 신속성(실시간 방송, 온라인 게임 등에서 사용)

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
