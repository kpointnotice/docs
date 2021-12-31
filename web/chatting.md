# 채팅 기능
 
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
  
  <mark style="color:red;">**roomId / tartget 중 하나는 필수**</mark>

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|            message            |          String           |                Y               |          채팅 메시지           |            Hello!             | 
|            roomId             |          String           |                N               |   해당 roomId로 메시지 전송     |           K43254033           | 
|            target             |          String           |                N               |   해당 userId에게 메시지 전송   |           kpoint123           | 

- **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))