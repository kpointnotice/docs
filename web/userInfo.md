# 사용자 정보 관련 기능

## 사용자 정보 변경

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.editUserInfo('홍길동', true, false);
```
{% endcode %}



* **타입**

```typescript
editUserInfo(
    name?: string;
    video?: boolean;
    audio?: boolean;
    broadcast?: boolean;
    target?: boolean;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**\
  <mark style="color:red;">**name / video / audio 중 하나는 필수**</mark>

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>name</td><td>유저 닉네임</td><td>'홍길동'</td></tr><tr><td>video</td><td>비디오 활성화 여부</td><td>true</td></tr><tr><td>audio</td><td>오디오 활성화 여부</td><td>true</td></tr><tr><td>broadcast</td><td><ul><li>true: 방에 <a href="event.md#type-edituserinfo">editUserInfo 이벤트 메시지</a>로 수정 알림 </li><li>false: 미알림</li></ul></td><td>true</td></tr><tr><td>target</td><td>p2p시 상대방 아이디</td><td>true</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>



