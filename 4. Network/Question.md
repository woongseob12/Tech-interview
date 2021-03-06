**연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?**

`Client가 데이터 전송을 마쳤다고 하더라고 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다`

---

**FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하게 된다면?**

```
이러한 현상을 대비하기 위해 양측은 FIN 플래그를 수신하더라도 일정시간(Default: 240sec)동안 세션을 남겨 놓고 잉여 패킷을 기다리는 과정을 거침`

Server: CLOSE_WAIT
Client: TIME_WAIT
```

---

**초기 Sequence Number인 ISN이 난수인 이유는?**

```
Connection을 맺을 때 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용된다.

따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재한다

서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 숫자일 경우 이전 Connection으로 부터 오는 패킷으로 인식할 수 있기 때문에 난수로 설정한다.
```