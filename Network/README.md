##### 순서

1. 3-Way handshake
2. Cookie, Session
3. HTTP, HTTPS
4. OSI 7 Layer
5. REST & RESTful
6. TCP
7. UDP
8. 공개키, 대칭키
9. 로드 밸런싱
10. URI, URL, URN
11. 웹의 흐름

<br>

<br>

# 3-Way handshke

- TCP/IP 프로토콜을 이용하여 통신을 진행할 때, 두 종간 단 **정확한** 데이터 전송을 보장하기 위해 연결을 설정하는 과정
- **실제로 데이터 전달이 시작하기 전에 한쪽이, 다른 한쪽이 준비 되었다는 것을 알 수 있도록 함**

<BR>

**실행 과정**

- SYN : Synchronize Sequence Number
- ACK : Acknowledgement
- Client -> Server : TCP SYN
- Server -> Client : TCP SYN ACK
- Client -> Server : TCP ACK

<br>

![](https://user-images.githubusercontent.com/33534771/75338886-d77ea880-58d2-11ea-84c3-f8b60663f9c6.png)



1. 클라이언트는 서버에 접속을 요청하는 SYN 패킷 전송. 이때 ***클라이언트는 SYN을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태***
2. 서버는 SYN 요청을 받고 클라이언트에게 요청을 수락한다는 ACK와 SYN flag 가 설정된 패킷을 발송. 이때 ***서버는 클라이언트가 다시 ACK로 응답(전송)하기를 기다리는 SYN_RECEIVED 상태***
3. 클라이언트가 서버에게 ACK를 보내고 이후로ㅜ터는 연결이 이루어지고 데이터가 오고 감. 이때 ***서버는 ESTABLISHED 상태***

<br>

**2-Way가 아닌 3-Way 인 이유**

- TCP는 **양방향 연결**이기 때문에 클라이언트에서 서버에게 자신의 존재를 알리고 패킷을 보낼 수 있는 것처럼, 서버에서도 클라이언트에게 자신의 존재를 알리고 패킷을 보낼 수 있다는 신호를 보내야 하기 때문

<br>

<br>

# 4-Way handshake

- TCP/IP 프로토콜을 이용한 통신 과정에서는 3-Way handshake를 통해 연결을 설정, 4-Way handshake를 통해 연결 설정을 해제

<br>

![](https://user-images.githubusercontent.com/33534771/75338959-ef562c80-58d2-11ea-99eb-1c09ec97e83a.png)

**실행 과정**

1. 클라이언트는 서버에게 연결을 종료하겠다는 FIN 전송
2. 서버는 클라이언트의 요청(FIN)에 대한 응답으로 ACK 전송
3. **처리해야 할 자신의 통신이 끝날 때 까지 기다림**
4. 처리해야 할 모든 통신을 끝마쳤다면, 연결을 종료하겠다는 FIN 전송
5. 클라이언트는 FIN 패킷에 대한 확인 응답으로 ACK 전송
6. 클라이언트의 ACK를 받은 서버는 소켓 연결을 close
7. **클라이언트는 아직 서버로부터 받지 못한 데이터가 있을 것을 대비해 기다림(TIME_WAIT, Default = 240초)**

