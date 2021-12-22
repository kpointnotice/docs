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

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              name             |          String           |                N               |         사용자 닉네임         |              홍길동             |
|             video             |          Boolean          |                N               |          video 정보           |               true             |
|             audio             |          Boolean          |                N               |          audio 정보           |               true             |

- **응답**

  응답 코드 리턴