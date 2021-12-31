# API 명세서

### 세션 연결(register)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|            cpCode              |            String             |             Y             |         라이센스 인증 코드         |
|            ipAddr              |            String             |             Y             |         사용자의 ip 주소           |
|            authKey             |            String             |             Y             |          라이센스 인증 키          |
|            userId              |            String             |             N             |          사용자의 userId          |
|             name               |            String             |             N             |          사용자의 닉네임          |
|            device              |            String             |             N             |           사용자의 기기           |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      cpCode: "KP-123",
      ipAddr: "ip address..",
      authKey: "auth key..",
      userId: "kpoint123",
      name: "홍길동",
      device: "Galaxy Tab"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### P2P통화 방 만들기(createRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             N             |            방의 roomId           |
|             title              |            String             |             N             |             방의 제목             |
|            capacity            |            number             |             N             |             최대 인원             |
|            destroy             |           Boolean             |             Y             |       아무도 없을 시, 방 종료      |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033",
      title: "chatRoom"
      capacity: 5,
      destroy: "false"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 그룹통화 방 만들기(createVideoRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             N             |            방의 roomId           |
|             title              |            String             |             N             |             방의 제목             |
|            capacity            |            number             |             N             |             최대 인원             |
|            destroy             |           Boolean             |             Y             |       아무도 없을 시, 방 종료      |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033",
      title: "chatRoom"
      capacity: 5,
      destroy: "false"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방 종료(destroyRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id     |
|            userId              |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |            방의 roomId           |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방 입장(joinRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|            userId              |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |            방의 roomId           |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방 퇴장(leaveRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id     |
|            userId              |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |            방의 roomId           |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 방의 영상 정보(sdpRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |
|              sdp               |            Object             |             Y             |              SDP 정보             |
|             type               |            String             |             N             |         cam / screen 구분         |
|            target              |            String             |             N             |          상대방의 userId          |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
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
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### SDP 전송 요청(sdp)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             N             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|              sdp               |            Object             |             Y             |             SDP 정보              |
|             type               |            String             |             Y             |         cam / screen 구분         |
|            target              |            String             |             N             |          상대방의 userId          |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
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
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 상대방의 영상 가져오기(subscribe)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |
|             type               |            String             |             Y             |         cam / screen 구분         |
|            target              |            String             |             Y             |          상대방의 userId          |
|             video              |           Boolean             |             Y             |             영상 권한             |
|             audio              |           Boolean             |             Y             |             음성 권한             |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
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
|            eventOp             |          String           |             이벤트 op             |
|              code              |           String          |              응답 코드            |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 공유 화면(screen)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             이벤트 op             |
|              code              |           String          |              응답 코드            |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 화이트보드(whiteboard)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             이벤트 op             |
|              code              |           String          |              응답 코드            |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 자료 정보(document)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             이벤트 op             |
|              code              |           String          |              응답 코드            |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 자료 공유(documentShare)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |
|              img               |            String             |             Y             |           이미지 정보              |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033",
      img: "imgURL"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |             응답 코드             |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 그리기 시작(drawing)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             userId             |            String             |             Y             |          사용자의 userId          |
|             roomId             |            String             |             Y             |           방의 roomId             |
|              xy                |            Object             |             N             |          그리기 위치 정보          |
|             tool               |            String             |             N             |       그리기 도구(pen, eraser)    |
|             color              |            String             |             N             |          색깔(pen, eraser)       |
|          strokeWidth           |            number             |             N             |          그리기 도구 굵기         |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
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
|            eventOp             |           String          |             이벤트 op             |
|             code               |           String          |              응답 코드            |
|            message             |           String          |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))

### 공유 종료(shareStop)
요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|            userId              |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             Y             |           방의 roomId             |



샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      userId: "kpoint123",
      roomId: "K43254033"
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |          String           |             이벤트 op             |
|              code              |          String           |             응답 코드             |
|            message             |          String           |            응답 메시지            |

샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      code: "200",
      message: "ok"
  }
```
{% endcode %}

성공(200, ok)가 아닌 경우에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](../web/code.md))