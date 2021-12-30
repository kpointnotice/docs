# API 명세서

### 세션 연결(register)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |      요청/응답 매칭을 위한 id      |
|             cpCode             |            String             |             Y             |         라이센스 인증 코드         |
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
      ipAddr: "ip..",
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

### P2P통화 방 만들기(createRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             N             |            방의 roomId           |
|             title              |            String             |             N             |              방의 제목            |
|            capacity            |            number             |             N             |              최대 인원            |
|            destroy             |           Boolean             |             Y             |                  -               |



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
      destroy: ""
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

### 그룹통화 방 만들기(createVideoRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
|            roomId              |            String             |             N             |            방의 roomId           |
|             title              |            String             |             N             |              방의 제목            |
|            capacity            |            number             |             N             |              최대 인원            |
|            destroy             |           Boolean             |             Y             |                  -               |



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
      destroy: ""
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

### 방 종료(destroyRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
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

### 방 입장(joinRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
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

### 방 퇴장(leaveRoom)

요청
| <center>**Parameter**</center> |  <center>**Type**</center>  |<center>**Required**</center>| <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            String             |             Y             |             이벤트 op             |
|             reqId              |            String             |             Y             |       요청/응답 매칭을 위한 id      |
|             userId             |            String             |             Y             |          사용자의 userId          |
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