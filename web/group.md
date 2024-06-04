# 분반 기능

## 분반 시작

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.createGroup(['kpoint123', 'knowledge123'], '분반명');
```
{% endcode %}



* **타입**

```typescript
createGroup(
    list?: string[];
    title?: string;
): Promise<{
    groupId: string;
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>list</td><td><ul><li>분반에 참여할 사용자들</li><li>list 유저들에게 <a href="event.md#type-creategroup">createGroup 이벤트 메시지</a> 보냄<br>메시지 받으면 사용자는 기존 방에서 <a href="room.md#undefined-2">leaveRoom</a> 한 뒤 분반 아이디로 <a href="room.md#undefined-1">joinRoom</a> 해 분반에 참여</li><li>생략시 분반 방만 생성</li></ul></td><td>['kpoint123', 'knowledge123']</td></tr><tr><td>title</td><td>방 제목</td><td>'분반명'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>groupId</td><td>분반 방 아이디</td><td>'r1196417'</td></tr></tbody></table>





## 분반 종료

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.endGroup(groupId);
```
{% endcode %}



* **타입**

```typescript
endGroup(
    groupId: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>groupId</td><td><ul><li>메인 룸에서 호출</li><li>분반 destrory</li></ul></td><td>'r1196417'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>



