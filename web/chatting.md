# 채팅 기능

메시지 전송 기능에는 

<hr>
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

<table style="text-align:center;">
    <tr>
        <td>파라미터</td>
        <td>타입</td>
        <td>필수 여부</td>
        <td>설명</td>
        <td>예시</td>
    </tr>
    <tr>
        <td>message</td>
        <td>String</td>
        <td>Y</td>
        <td>채팅 메시지</td>
        <td>Hello!</td>
    </tr>
    <tr>
        <td>roomId</td>
        <td>String</td>
        <td rowspan="2">둘 중 하나는 필수</td>
        <td>해당 roomId로 메시지 전송</td>
        <td>K43254033</td>
    </tr>
    <tr>
        <td>target</td>
        <td>String</td>
        <td>해당 userId에게 메시지 전송</td>
        <td>kpoint123</td>
    </tr>
</table>


- **응답**

    응답 코드 리턴

<!--
    <mark style="color:red;">**채팅 방으로 전체 메시지를 **</mark>

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|            message            |          String           |                Y               |          채팅 메시지           |            Hello!             | 
|            roomId             |          String           |                N               |   해당 roomId로 메시지 전송     |           K43254033           | 
|            target             |          String           |                N               |   해당 userId에게 메시지 전송   |           kpoint123           | 

--!>