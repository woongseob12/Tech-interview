# Network

## Index<br>

<ol>
    <li>OSI 7 Layer</li>
    <li>GET & POST</li>
    <li>TCP 3-way handshake & 4-way hand shake</li>
    <li>TCP/ UDP</li>
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
