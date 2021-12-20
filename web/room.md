# 방 관련 기능

## 방 생성(P2P)

{% code title="index.js" %}
```javascript
// 방
await knowledgetalk.createRoom('room1', 'title');
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 |  예시  |             설명             |
| :------: | :----: | :-------: | :----: | :--------------------------: |
|  roomId  | string |     N     | room1  |   원하는 ROOM ID로 방 생성   |
|  title   | string |     N     | 방제목 | 원하는 ROOM TITLE 로 방 생성 |

- **응답**

| 파라미터 |  타입  | 필수 여부 | 예시  |                   설명                   |
| :------: | :----: | :-------: | :---: | :--------------------------------------: |
|  roomId  | string |     N     | room1 | 사용자가 요청한 ID 또는 서버가 생성한 ID |

실패 시, error code 리턴

## 방 생성(N:N)

{% code title="index.js" %}
```javascript
//성공 시, room id 리턴
await knowledgetalk.createVideoRoom('room1', 'title');
```
{% endcode %}

- **요청** 

| 파라미터 |  타입  | 필수여부 |  예시  |             설명             |
| :------: | :----: | :------: | :----: | :--------------------------: |
|  roomId  | string |    N     | room1  |   원하는 ROOM ID로 방 생성   |
|  title   | string |    N     | 방제목 | 원하는 ROOM TITLE 로 방 생성 |

- **응답**

| 파라미터 |  타입  | 필수 여부 | 예시  |                   설명                   |
| :------: | :----: | :-------: | :---: | :--------------------------------------: |
|  roomId  | string |     N     | room1 | 사용자가 요청한 ID 또는 서버가 생성한 ID |

실패 시, error code 리턴

## 방 입장

{% code title="index.js" %}
```javascript
//방 입장 요청
await knowledgetalk.joinroom('room1');
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 | 예시  |        설명        |
| :------: | :----: | :-------: | :---: | :----------------: |
|  roomId  | string |     Y     | room1 | 입장하려는 ROOM ID |

- **응답**

|  파라미터   |  타입  | 필수 여부 |               예시               |             설명             |
| :---------: | :----: | :-------: | :------------------------------: | :--------------------------: |
|   members   | object |     N     | { "kpoint": { "name": "익명" } } | 현재 방에 접속한 유저 리스트 |
| isRecording |  bool  |     Y     |              false               |        현재 녹화 여부        |
|    media    |  bool  |     Y     |              false               |    미디어 서버 사용 여부     |
|    title    | string |     Y     |            room title            |           방 제목            |
|    group    | object |     N     |                                  |          분반 정보           |

실패 시, error code 리턴

## 방 퇴장

{% code title="index.js" %}
```javascript
//퇴장 요청
await knowledgetalk.leaveRoom('room1');
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 | 예시  |        설명        |
| :------: | :----: | :-------: | :---: | :----------------: |
|  roomId  | string |     Y     | room1 | 퇴장하려는 ROOM ID |

- **응답**

  응답 코드 리턴

## 방 종료

{% code title="index.js" %}
```javascript
//방 종료 요청
await knowledgetalk.destroyRoom('room1');
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 | 예시  |        설명        |
| :------: | :----: | :-------: | :---: | :----------------: |
|  roomId  | string |     Y     | room1 | 종료하려는 ROOM ID |

- **응답**

  응답 코드 리턴

## 참여 인원 조회

{% code title="index.js" %}
```javascript
//멤버 리스트 조회
await knowledgetalk.memberList(roomId);
```
{% endcode %}
    

- **요청**

| 파라미터 |  타입  | 필수 여부 | 예시  |   설명    |
| :------: | :----: | :-------: | :---: | :-------: |
|  roomId  | string |     Y     | room1 | 룸 아이디 |

- **응답**

| 파라미터 |  타입  | 필수 여부 | 예시 |                설명                |
| :------: | :----: | :-------: | :--: | :--------------------------------: |
|   code   | string |     Y     | 200  |              응답코드              |
| members  | object |     Y     |      | KEY: 유저 아이디, VALUE: 유저 정보 |

## 권한 부여 기능

{% code title="index.js" %}
```javascript
//권한 부여(id, chat, draw, screen, whiteboard, document)
await knowledgetalk.permit('kpoint', true, null, null, null, null);
```
{% endcode %}


- **요청**

|  파라미터  |  타입   | 필수 여부 |  예시  |       설명       |
| :--------: | :-----: | :-------: | :----: | :--------------: |
|   target   | string  |     Y     | kpoint |     대상 ID      |
|    chat    | boolean |     N     |  true  |    채팅 권한     |
|    draw    | boolean |     N     |  true  |   그리기 권한    |
|   screen   | boolean |     N     |  true  |  화면공유 권한   |
| whiteboard | boolean |     N     |  true  | 화이트 보드 권한 |
|  document  | boolean |     N     |  true  |  자료공유 권한   |

<span style="color:red">**chat / draw / screen / whiteboard / document 중 하나는 필수**</span>

- **응답**

  응답 코드 리턴


## 알림 메시지 전송

## inform

{% code title="index.js" %}
```javascript
//알림 메시지(message, target, roomId)
await knowledgetalk.inform('message', 'kpoint');
```
{% endcode %}


| 파라미터 |  타입  | 필수 여부 |  예시  |            설명            |
| :------: | :----: | :-------: | :----: | :------------------------: |
| message  | string |     Y     | hello  |        전달 메시지         |
|  target  | string |     N     | kpoint | 해당 USER 에게 메시지 전송 |
|  roomId  | string |     N     | room1  | 해당 ROOM ID로 메시지 전송 |

- **응답**

  응답 코드 리턴