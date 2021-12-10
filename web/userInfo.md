# 사용자 정보 관련 기능

## 사용자 정보 변경

{% code title="index.js" %}
```javascript
//유저 정보 변경(name, video, audio)
await knowledgetalk.editUserInfo('kpoint', true, false);
```
{% endcode %}


- **요청**

| 파라미터 |  타입   | 필수 여부 |  예시  |    설명     |
| :------: | :-----: | :-------: | :----: | :---------: |
|   name   | string  |     N     | kpoint | 유저 닉네임 |
|  video   | boolean |     N     |  true  | video 정보  |
|  audio   | boolean |     N     |  true  | audio 정보  |

<span style="color:red">**name / video / audio 중 하나는 필수**</span>

- **응답**

  응답 코드 리턴