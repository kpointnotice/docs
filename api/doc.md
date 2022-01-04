# API 명세서

### 세션 연결(register)

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             cpCode             |          String           |               Y               |             cp code              |
|             ipAddr             |          String           |               Y               |            ip address            |
|            authKey             |          String           |               Y               |           license key            |
|             userId             |          String           |               N               |             user id              |
|              name              |          String           |               N               |            user name             |
|             device             |          String           |               N               |           device info            |

- **샘플**
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "abc123",
      cpCode: "KP-123",
      ipAddr: "ip address..",
      authKey: "auth key..",
      userId: "kpoint123",
      name: "홍길동",
      device: "Galaxy Tab"
  }
```
{% endcode %}

- **응답**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|             reqId              |          String           |          transaction id          |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |
|             userId             |          String           |             user id              |
|           iceServers           |           Array           |         ice server 정보          |

- **샘플**

{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "abc123",
      code: "200",
      message: "ok",
      userId: "kpoint12",
      iceServers: [
        {
            "urls": [
                "turn:dev.knowledgetalk.co.kr:46000"
            ],
            "username": "kpoint",
            "credential": "kpoint01"
        },
        {
            "urls": [
                "stun:dev.knowledgetalk.co.kr:46000"
            ]
        }
      ]
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### P2P통화 방 만들기(createRoom)

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               N               |             room id              |
|             title              |          String           |               N               |            room title            |
|            capacity            |          number           |               N               |      maximum room capacity       |
|            destroy             |          Boolean          |               Y               | if empty, room will be destroyed |

- **샘플**
  
{% code title="createRoom" %}
```json
  {
      eventOp: "createRoom",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      title: "chatRoom"
      capacity: 5,
      destroy: "false"
  }
```
{% endcode %}

- **응답**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|             reqId              |          String           |          transaction id          |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |
|             roomId             |          String           |             room id              |

- **샘플**

{% code title="createRoom" %}
```json
  {
    eventOp: "createRoom",
    reqId: "abc123",
    code: "200",
    message: "OK",
    roomId: "r6526119"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 그룹통화 방 만들기(createVideoRoom)

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               N               |             room id              |
|             title              |          String           |               N               |           room tittle            |
|            capacity            |          number           |               N               |      maximum room capacity       |
|            destroy             |          Boolean          |               Y               | if empty, room will be destroyed |

- **샘플**
  
{% code title="createRoom" %}
```json
  {
      eventOp: "createVideoRoom",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      title: "chatRoom"
      capacity: 5,
      destroy: "false"
  }
```
{% endcode %}

- **응답**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|             reqId              |          String           |          transaction id          |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |
|             roomId             |          String           |             room id              |

- 샘플

{% code title="createVideoRoom" %}
```json
  {
    eventOp: "createVideoRoom",
    reqId: "abc123",
    code: "200",
    message: "OK",
    roomId: "r6526119"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방 종료(destroyRoom)

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



- **샘플**

{% code title="destroyRoom" %}
```json
  {
      eventOp: "destroyRoom",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

- **응답**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|             reqId              |          String           |          transaction id          |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

- **샘플**

{% code title="destroyRoom" %}
```json
  {
      eventOp: "destroyRoom",
      reqId: "abc123",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방 입장(joinRoom)

- 요청

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



- 샘플
  
{% code title="joinRoom" %}
```json
  {
      eventOp: "joinRoom",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

- 응답

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|             reqId              |          String           |          transaction id          |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |
|            memebers            |          object           |       current members info       |
|          isRecording           |          boolean          |           if recording           |
|             media              |          boolean          |      if using media server       |
|             title              |          String           |            room title            |
|              host              |          object           |            host info             |

- 샘플

{% code title="joinRoom" %}
```json
  {
      eventOp: "joinRoom",
      code: "200",
      message: "ok"
      code: "200",
      roomId: "K43254033",
      members: {
          kpoint123: "user info..."
      },
      isRecording: false,
      media: true,
      title: "video room",
      host: "host info..."
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방 퇴장(leaveRoom)

- 요청

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



- 샘플

{% code title="leaveRoom" %}
```json
  {
      eventOp: "leaveRoom",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

- 응답

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|             reqId              |          String           |          transaction id          |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

- 샘플

{% code title="leaveRoom" %}
```json
  {
      eventOp: "leaveRoom",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방의 영상 정보(sdpRoom)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|              sdp               |          Object           |               Y               |             SDP 정보             |
|              type              |          String           |               N               |        cam / screen 구분         |
|             target             |          String           |               N               |         상대방의 userId          |



샘플
{% code title="sdpRoom" %}
```json
  {
      eventOp: "sdpRoom",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      sdp: "RTCSessionDescription {type: "answer", sdp: ...}",
      type: "cam",
      target: "knowledge123"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="sdpRoom" %}
```json
  {
      eventOp: "sdpRoom",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### SDP 전송 요청(sdp)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               N               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|              sdp               |          Object           |               Y               |             SDP 정보             |
|              type              |          String           |               Y               |        cam / screen 구분         |
|             target             |          String           |               N               |         상대방의 userId          |



샘플
{% code title="sdp" %}
```json
  {
      eventOp: "sdp",
      reqId: "abc123",
      userId: "kpoint123",
      sdp: "RTCSessionDescription {type: "answer", sdp: ...}",
      type: "cam",
      target: "knowledge123"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="sdp" %}
```json
  {
      eventOp: "sdp",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 상대방의 영상 가져오기(subscribe)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|              type              |          String           |               Y               |        cam / screen 구분         |
|             target             |          String           |               Y               |         상대방의 userId          |
|             video              |          Boolean          |               Y               |            영상 권한             |
|             audio              |          Boolean          |               Y               |            음성 권한             |



샘플
{% code title="subscribe" %}
```json
  {
      eventOp: "subscribe",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      type: "cam / screen 구분",
      target: "knowledge123"
      video: "true",
      audio: "true"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="subscribe" %}
```json
  {
      eventOp: "subscribe",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 공유 화면(screen)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



샘플
{% code title="screen" %}
```json
  {
      eventOp: "screen",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="screen" %}
```json
  {
      eventOp: "screen",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 화이트보드(whiteboard)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



샘플
{% code title="whiteboard" %}
```json
  {
      eventOp: "whiteboard",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="whiteboard" %}
```json
  {
      eventOp: "whiteboard",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 자료 정보(document)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



샘플
{% code title="document" %}
```json
  {
      eventOp: "document",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="document" %}
```json
  {
      eventOp: "document",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 자료 공유(documentShare)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|              img               |          String           |               Y               |           이미지 정보            |



샘플
{% code title="documentShare" %}
```json
  {
      eventOp: "documentShare",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      img: "imgURL"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="documentShare" %}
```json
  {
      eventOp: "documentShare",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 그리기 시작(drawing)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|               xy               |          Object           |               N               |         그리기 위치 정보         |
|              tool              |          String           |               N               |     그리기 도구(pen, eraser)     |
|             color              |          String           |               N               |        색깔(pen, eraser)         |
|          strokeWidth           |          number           |               N               |         그리기 도구 굵기         |



샘플
{% code title="drawing" %}
```json
  {
      eventOp: "drawing",
      userId: "kpoint123",
      roomId: "K43254033",
      xy: {x:"x축",y:"y축"},
      tool: "pen",
      color: "black",
      strokeWidth: "1"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="drawing" %}
```json
  {
      eventOp: "drawing",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 공유 종료(shareStop)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



샘플
{% code title="shareStop" %}
```json
  {
      eventOp: "shareStop",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="shareStop" %}
```json
  {
      eventOp: "shareStop",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 닉네임 변경(changeName)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |



샘플
{% code title="changeName" %}
```json
  {
      eventOp: "changeName",
      reqId: "abc123",
      userId: "kpoint123"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="changeName" %}
```json
  {
      eventOp: "changeName",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 채팅 보내기(chat)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             target             |          String           |               N               |         상대방의 userId          |
|             roomId             |          String           |               N               |             room id              |
|            message             |          String           |               Y               |       보내고자 하는 메시지       |



샘플
{% code title="chat" %}
```json
  {
      eventOp: "chat",
      reqId: "abc123",
      userId: "kpoint123",
      target: "knowledge123",
      roomId: "K43254033",
      message: "Hello!"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="chat" %}
```json
  {
      eventOp: "chat",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 그리기 허용(permit)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|             reqId              |          String           |               Y               |          transaction id          |
|             target             |          String           |               Y               |         상대방의 userId          |
|              chat              |          Boolean          |               N               |            채팅 권한             |
|              draw              |          Boolean          |               N               |           그리기 권한            |
|             screen             |          Boolean          |               N               |            영상 권한             |
|           whiteboard           |          Boolean          |               N               |         화이트보드 권한          |
|            document            |          Boolean          |               N               |          자료 공유 권한          |



샘플
{% code title="permit" %}
```json
  {
      eventOp: "permit",
      userId: "kpoint123",
      roomId: "K43254033",
      reqId: "abc123",
      target: "knowledge123",
      chat: "true",
      draw: "true",
      screen: "false",
      whiteboard: "true",
      document: "false"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="permit" %}
```json
  {
      eventOp: "permit",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 사용자 정보 변경(editUserInfo)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|              name              |          String           |               N               |            user name             |
|             video              |          Boolean          |               N               |            영상 허용             |
|             audio              |          Boolean          |               N               |            음성 허용             |
|           broadcast            |          Boolean          |               N               |        브로드캐스트 허용         |



샘플
{% code title="editUserInfo" %}
```json
  {
      eventOp: "editUserInfo",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      name: "홍길동",
      video: "true",
      audio: "true",
      broadcast: "false"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="editUserInfo" %}
```json
  {
      eventOp: "editUserInfo",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방에 접속한 유저 조회(memberList)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |



샘플
{% code title="memberList" %}
```json
  {
      eventOp: "memberList",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="memberList" %}
```json
  {
      eventOp: "memberList",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 분반 시작(createGroup)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|              list              |           Array           |               N               |          사용자 리스트           |
|             title              |          String           |               N               |            방의 제목             |



샘플
{% code title="createGroup" %}
```json
  {
      eventOp: "createGroup",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      list: ["kpoint123", "knowledge123"],
      title: "chatGroup"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="createGroup" %}
```json
  {
      eventOp: "createGroup",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 분반 종료(endGroup)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             roomId             |          String           |               Y               |             room id              |
|            groupId             |          String           |               Y               |          분반의 groupId          |



샘플
{% code title="endGroup" %}
```json
  {
      eventOp: "endGroup",
      reqId: "abc123",
      userId: "kpoint123",
      roomId: "K43254033",
      groupId: "knowledgeGroup"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="endGroup" %}
```json
  {
      eventOp: "endGroup",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 후보자 선정(candidate)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: |
|            eventOp             |          String           |               Y               |             op name              |
|             reqId              |          String           |               Y               |          transaction id          |
|             userId             |          String           |               Y               |             user id              |
|             target             |          String           |               Y               |         상대방의 userId          |
|           candidate            |            any            |               Y               |           후보자 정보            |
|              type              |          String           |               Y               |               타입               |
|              cam               |          Boolean          |               Y               |        cam / stream 구분         |



샘플
{% code title="candidate" %}
```json
  {
      eventOp: "candidate",
      reqId: "abc123",
      userId: "kpoint123",
      target: "knowledge123",
      candidate: "candidateObject",
      type: "candidateType", 
      cam: "stream"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             op name              |
|              code              |          String           |          response code           |
|            message             |          String           |         response message         |

샘플
{% code title="candidate" %}
```json
  {
      eventOp: "candidate",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

