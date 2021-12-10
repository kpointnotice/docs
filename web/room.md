# 방 관련 기능

## 방 생성(P2P)

{% code title="index.js" %}
```javascript
//성공 시, room id 리턴
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