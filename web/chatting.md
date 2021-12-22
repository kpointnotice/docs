# 채팅 기능

<br>

## 채팅 메시지 전송

{% code title="index.js" %}
```javascript
// 채팅 메시지 전송(message, roomId, (target)) - 해당 roomId의 방 전체에 메시지 보내기 (undefined 생략 가능)
await knowledgetalk.chat('Hello!', 'K43254033', (undefined));

// 채팅 메시지 전송(message, undefined, target) - 해당 userId에게 메시지 보내기
await knowledgetalk.chat('Hello!', undefined, 'kpoint123');

// 채팅 메시지 전송(message, roomId, target) - 해당 roomId의 방 전체와 userId에게 전부 보내기
await knowledgetalk.chat('Hello!', 'K43254033', 'kpoint123');
```
{% endcode %}

- **요청**
- <mark style="color:red;">**rwoomId / tartget 중 하나는 필수**</mark>

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|            message            |          String           |                Y               |          채팅 메시지           |            Hello!             | 
|            roomId             |          String           |               Y/N              |   해당 roomId로 메시지 전송     |           K43254033           | 
|            target             |          String           |               Y/N              |   해당 userId에게 메시지 전송   |           kpoint123           | 

- **응답**

    응답 코드 리턴