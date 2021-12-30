# 방 관련 기능
 
## P2P 방 생성

{% code title="index.js" %}
```javascript
// P2P 방 생성(roomId, title, capacity, detroy)
await knowledgetalk.createRoom('K43254033', 'chatRoom');
```
{% endcode %}

- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               N                |       요청할 roomId       |         K43254033         |
|             title             |          String           |               N                |          방 제목          |         chatRoom          |
|           capacity            |          number           |               N                |         수용인원          |            16             |
|            destroy            |          Boolean          |               N                |  아무도 없을 시, 방 종료  |           false           |

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               N                |  랜덤 또는 요청된 roomId  |         chatRoom          |
 
## 그룹통화 방 생성

{% code title="index.js" %}
```javascript
// 그룹통화 방 생성(roomId, title)
await knowledgetalk.createVideoRoom('K43254033', 'chatRoom');
```
{% endcode %}

* **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               N                |       요청할 roomId       |         K43254033         |
|             title             |          String           |               N                |          방 제목          |         chatRoom          |
|           capacity            |          number           |               N                |         수용인원          |            16             |
|            destroy            |          Boolean          |               N                |  아무도 없을 시, 방 종료  |           false           |

- **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))
    
| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               N                |  랜덤 또는 요청된 roomId  |         chatRoom          |
 
## 방 입장

{% code title="index.js" %}
```javascript
// 방 입장(roomId)
await knowledgetalk.joinroom('K43254033');
```
{% endcode %}

* **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               Y                |     입장하려는 roomId     |         K43254033         |

* **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center>  |     <center>**예시**</center>     |
| :---------------------------: | :-----------------------: | :----------------------------: | :------------------------: | :-------------------------------: |
|            members            |          Object           |               N                | 현재 방에 접속한 유저 정보 | "kpoint123": { "name": "홍길동" } |
|          isRecording          |          Boolean          |               Y                |       현재 녹화 여부       |               true                |
|             media             |          Boolean          |               Y                |   미디어 서버 사용 여부    |               true                |
|             title             |          String           |               Y                |          방 제목           |             chatRoom              |
|             group             |          Object           |               N                |         분반 정보          |                                   |
 
## 방 퇴장

{% code title="index.js" %}
```javascript
// 방 퇴장(roomId)
await knowledgetalk.leaveRoom('K43254033');
```
{% endcode %}

* **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               Y                |     퇴장하려는 roomId     |         K43254033         |

*   **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))
 
## 방 종료

{% code title="index.js" %}
```javascript
// 방 종료(roomId)
await knowledgetalk.destroyRoom('K43254033');
```
{% endcode %}

* **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               Y                |     종료하려는 roomId     |         K43254033         |

*   **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))
 
## 방에 접속한 유저 조회

{% code title="index.js" %}
```javascript
// 방에 접속한 유저 조회(roomId)
await knowledgetalk.memberList(roomId);
```
{% endcode %}

* **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            roomId             |          String           |               Y                |     종료하려는 roomId     |         K43254033         |

* **응답**
  
  성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> |     <center>**예시**</center>     |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-------------------------------: |
|            members            |          Object           |               Y                | 현재 방에 접속한 members  | "kpoint123": { "name": "홍길동" } |
 
## 권한 부여

{% code title="index.js" %}
```javascript
// 권한 부여(userId, chat, draw, screen, whiteboard, document)
await knowledgetalk.permit('kpoint123', true, true, true, true, true);
```
{% endcode %}

* **요청**
  
  <mark style="color:red;">**chat / draw / screen / whiteboard / document 중 하나는 필수**</mark>

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            target             |          String           |               Y                |        상대 userId        |         kpoint123         |
|             chat              |          Boolean          |               N                |         채팅 권한         |           true            |
|             draw              |          Boolean          |               N                |        그리기 권한        |           true            |
|            screen             |          Boolean          |               N                |       화면공유 권한       |           true            |
|          whiteboard           |          Boolean          |               N                |      화이트보드 권한      |           true            |
|           document            |          Boolean          |               N                |       자료공유 권한       |           true            |

*   **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))
  
## 알림 메시지 전송

{% code title="index.js" %}
```javascript
// 알림 메시지 전송(message, target, roomId)
await knowledgetalk.inform('Hello!', 'kpoint123', 'K43254033');
```
{% endcode %}

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> | <center>**설명**</center> | <center>**예시**</center> |
| :---------------------------: | :-----------------------: | :----------------------------: | :-----------------------: | :-----------------------: |
|            message            |          String           |               Y                |       전달할 메시지       |          Hello!           |
|            target             |          String           |               N                |  메시지를 전달할 userId   |         kpoint123         |
|            roomId             |          String           |               N                |  메시지를 전달할 roomId   |         K43254033         |

*   **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))
