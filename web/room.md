# 방 관련 기능

## P2P 방 생성

{% code title="index.js" %}
```javascript
// P2P 방 생성(roomId, title)
await knowledgetalk.createRoom('K43254033', 'chatRoom123');
```
{% endcode %}

- **요청**

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> | <center>설명</center> | <center>예시</center> |
| :-----------------------: | :-------------------: | :-----------------------: | :-------------------: | :------------------: |
|           roomId          |         String        |              N            |     요청할 roomId     |       K43254033      |
|           title           |         String        |              N            |        방 제목        |      chatRoom123     |

- **응답**

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> | <center>설명</center> | <center>예시</center> |
| :----------------------: | :-------------------: | :-----------------------: | :--------------------: | :-------------------: |
|           roomId         |         String        |             N             | 랜덤 또는 요청된 roomId |      chatRoom123      |

실패 시, error code 리턴

## 그룹통화 방 생성

{% code title="index.js" %}
```javascript
// 그룹통화 방 생성(roomId, title)
await knowledgetalk.createVideoRoom('K43254033', 'chatRoom123');
```
{% endcode %}

- **요청**  

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> | <center>설명</center> | <center>예시</center> |
| :-----------------------: | :-------------------: | :-----------------------: | :-------------------: | :------------------: |
|           roomId          |         String        |              N            |     요청할 roomId     |       K43254033      |
|           title           |         String        |              N            |        방 제목        |      chatRoom123     |

- **응답**

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> | <center>설명</center> | <center>예시</center> |
| :----------------------: | :-------------------: | :-----------------------: | :--------------------: | :-------------------: |
|           roomId         |         String        |             N             | 랜덤 또는 요청된 roomId |      chatRoom123      |

성공 시, room id 리턴
실패 시, error code 리턴

## 방 입장

{% code title="index.js" %}
```javascript
// 방 입장(roomId)
await knowledgetalk.joinroom('K43254033');
```
{% endcode %}

- **요청**

| <center>파라미터</center> |  <center>타입</center>  | <center>필수 여부</center> | <center>설명</center>  |        <center>예시</center>        |
| :----------------------: | :---------------------: | :------------------------: | :-------------------: | :---------------------------------: |
|          roomId          |          String         |              Y             |    입장하려는 roomId   |             K43254033             |

- **응답**

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> |     <center>설명</center>     |       <center>예시</center>       |
| :----------------------: | :-------------------: | :------------------------: | :--------------------------: | :-------------------------------: |
|          members         |         Object        |              N             |   현재 방에 접속한 유저 정보   | "kpoint123": { "name": "홍길동" } |
|        isRecording       |        Boolean        |              Y             |         현재 녹화 여부        |                true               |
|           media          |        Boolean        |              Y             |      미디어 서버 사용 여부     |                true               |
|           title          |         String        |              Y             |            방 제목            |            chatRoom123            |
|           group          |         Object        |              N             |           분반 정보           |                                   |

실패 시, error code 리턴

## 방 퇴장

{% code title="index.js" %}
```javascript
// 방 퇴장(roomId)
await knowledgetalk.leaveRoom('K43254033');
```
{% endcode %}

- **요청**

| <center>파라미터</center> |  <center>타입</center>  | <center>필수 여부</center> | <center>설명</center>  |        <center>예시</center>        |
| :-----------------------: | :--------------------: | :------------------------: | :--------------------: | :--------------------------------: |
|          roomId          |          String         |              Y             |        K43254033       |          퇴장하려는 roomId          | 

- **응답**

  응답 코드 리턴

## 방 종료

{% code title="index.js" %}
```javascript
// 방 종료(roomId)
await knowledgetalk.destroyRoom('K43254033');
```
{% endcode %}

- **요청**

| <center>파라미터</center> |  <center>타입</center>  | <center>필수 여부</center> |  <center>설명</center>  | <center>예시</center> |
| :-----------------------: | :--------------------: | :------------------------: | :--------------------: | :-------------------: |
|          roomId          |          String         |              Y             |        K43254033       |    종료하려는 roomId   | 

- **응답**

  응답 코드 리턴

## 방에 접속한 유저 조회

{% code title="index.js" %}
```javascript
// 방에 접속한 유저 조회(roomId)
await knowledgetalk.memberList(roomId);
```
{% endcode %}
    
- **요청**

| <center>파라미터</center> |  <center>타입</center>  | <center>필수 여부</center> |  <center>설명</center>  | <center>예시</center> |
| :----------------------: | :---------------------: | :------------------------: | :--------------------: | :-------------------: |
|          roomId          |          String         |              Y             |        K43254033       |    종료하려는 roomId   | 

- **응답**

| <center>파라미터</center> |  <center>타입</center>  | <center>필수 여부</center> |     <center>설명</center>     |       <center>예시</center>       |
| :-----------------------: | :--------------------: | :------------------------: | :--------------------------: | :-------------------------------: |
|          members          |          Object        |              Y             |   현재 방에 접속한 members   | "kpoint123": { "name": "홍길동" } |

응답 코드 리턴, 성공시 200

## 권한 부여

{% code title="index.js" %}
```javascript
// 권한 부여(id, chat, draw, screen, whiteboard, document)
await knowledgetalk.permit('kpoint123', true, true, true, true, true);
```
{% endcode %}

- **요청**

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> | <center>설명</center> | <center>예시</center> |
| :-----------------------: | :------------------: | :------------------------: | :-------------------: | :-------------------: |
|           target          |        String        |              Y             |      상대 userId      |       kpoint123       |
|            chat           |        Boolean       |              N             |       채팅 권한       |         true          |
|            draw           |        Boolean       |              N             |      그리기 권한      |         true          |
|           screen          |        Boolean       |              N             |     화면공유 권한     |         true          |
|         whiteboard        |        Boolean       |              N             |    화이트보드 권한    |         true          |
|          document         |        Boolean       |              N             |     자료공유 권한     |         true          |

<br><br><br><br><br><br><br>
// testing......
<hr>
<span style="color:red">**chat / draw / screen / whiteboard / document 중 하나는 필수**</span>
<hr>
<font color="red">"폰트"</font>
<hr>
<font color='red'>'폰트'</font>
<hr>
<h2 style="color:red">h2</h2>
<hr>
<h2><font color="red">h2</font></h2>
<hr>
<h2><span style="color:red">스팬 컬러레드</span></h2>
<hr>
<br><br><br><br><br><br><br>

- **응답**

  응답 코드 리턴

## 알림 메시지 전송

{% code title="index.js" %}
```javascript
// 알림 메시지(message, target, roomId)
await knowledgetalk.inform('Hello!', 'kpoint123', 'K43254033');
```
{% endcode %}

| <center>파라미터</center> | <center>타입</center> | <center>필수 여부</center> |  <center>설명</center> | <center>예시</center> |
| :----------------------: | :-------------------: | :------------------------: | :-------------------: | :-------------------: |
|          message         |         String        |              Y             |      전달할 메시지     |        Hello!         |
|          target          |         String        |              N             | 메시지를 전달할 userId |       kpoint123       |
|          roomId          |         String        |              N             | 메시지를 전달할 roomId |       K43254033       |

- **응답**

  응답 코드 리턴