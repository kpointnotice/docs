# 채팅 기능

## 채팅 메시지 전송

* **예시**

{% code title="index.js" %}
```javascript
// 해당 roomId의 방 전체에 메시지 보내기
await knowledgetalk.chat('Hello!', 'K43254033');

// 해당 userId에게 메시지 보내기
await knowledgetalk.chat('Hello!', undefined, 'kpoint123');

// 해당 roomId의 방 전체와 userId에게 전부 보내기
await knowledgetalk.chat('Hello!', 'K43254033', 'kpoint123');
```
{% endcode %}



* **타입**

```typescript
chat(
    message: string;
    roomId?: string;
    userId?: string;
): Promise<ResponseCode>;
```



*   **요청 상세**

    <mark style="color:red;">**roomId / tartget 중 하나는 필수**</mark>

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>message</td><td>채팅 메시지</td><td>'Hello!'</td></tr><tr><td>roomId</td><td>해당 roomId로 메시지 전송</td><td>'K43254033'</td></tr><tr><td>userId</td><td>해당 userId에게 메시지 전송</td><td>'kpoint123'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* 타겟 유저는 [chat 이벤트 메시지](event.md#type-chat)를 받아 사용

