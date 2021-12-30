# API 명세서

### 세션 연결(register)

요청
| <center>**Parameter**</center> | <center>**Required**</center> | <center>**Type**</center> | <center>**Description**</center> |
| :----------------------------: | :---------------------------: | :-----------------------: | :------------------------------: |
|            eventOp             |            string             |             Y             |            이벤트 op             
|             reqId              |            String             |             Y             |             요청/응답 매칭을 위한 id          
|             cpCode              |            String             |             Y             |             라이센스 인증 코드        
|             authKey              |            String             |             Y             |             라이센스 인증 키      


샘플
{% code title="register" %}
```json
  {
      eventOp: 'register',
      reqId: 'randomstring',
      cpCode: 'KP-123',
      authKey: 'auth key...'
  }
```
{% endcode %}

응답


### P2P통화 방 만들기(createRoom)

### 그룹통화 방 만들기(createVideoRoom)

### 방 입장(joinRoom)