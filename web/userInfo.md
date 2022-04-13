# 사용자 정보 관련 기능
 
## 사용자 정보 변경

{% code title="index.js" %}
```javascript
// 사용자 정보 변경(name, video, audio)
await knowledgetalk.editUserInfo('홍길동', true, false);
```
{% endcode %}

- **요청**

  <mark style="color:red;">**name / video / audio 중 하나는 필수**</mark>

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> |       <center>**Description**</center>       | <center>**Example**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------------------: | :--------------------------: |
|              name              |          String           |               N               |                사용자 닉네임                 |            홍길동            |
|             video              |          Boolean          |               N               |                  video 정보                  |             true             |
|             audio              |          Boolean          |               N               |                  audio 정보                  |             true             |
|           broadcast            |          Boolean          |               N               |     방에 정보 수정 알림 메시지 전송 여부     |             true             |
|             target             |          Boolean          |               N               | 특정 상대와의 p2p피어 연결 시, 상대방 아이디 |             true             |

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))