# API 명세서

### 세션 연결(register)

요청
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            string             |             Y             |            이벤트 op             |
|             reqId              |            String             |             Y             |     요청/응답 매칭을 위한 id     |
|             cpCode             |            String             |             Y             |        라이센스 인증 코드        |
|            authKey             |            String             |             Y             |         라이센스 인증 키         |


샘플
{% code title="register" %}
```json
  {
      eventOp: "register",
      reqId: "randomstring",
      cpCode: "KP-123",
      authKey: "auth key.."
  }
```
{% endcode %}

응답
| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |             String             |            이벤트 op             |
|             code              |             String            |     응답 코드    |
|             message             |             String             |        응답 메시지        |

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

### 그룹통화 방 만들기(createVideoRoom)

### 방 입장(joinRoom)