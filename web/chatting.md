# 채팅 기능

## 채팅 메시지 전송

{% code title="index.js" %}
```javascript
//채팅 메시지 전송(message, roomId, target)
await knowledgetalk.chat('message', 'room1');
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 |  예시  |            설명            |
| :------: | :----: | :-------: | :----: | :------------------------: |
| message  | string |     Y     | hello  |        채팅 메시지         |
|  roomId  | string |     N     | room1  | 해당 ROOM ID로 메시지 전송 |
|  target  | string |     N     | kpoint | 해당 USER 에게 메시지 전송 |

<span style="color:red">**roomId / target 중 하나는 필수**</span>

- **응답**

  응답 코드 리턴