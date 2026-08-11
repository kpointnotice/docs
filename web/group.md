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



---

## 시나리오: 분반 이동 (생성 → 입장 → 종료)

`createGroup`만으로 참가자가 자동 이동하지 않습니다. **list에 포함된 클라이언트는 presence를 받은 뒤** 메인 룸을 나와 분반 `groupId`로 다시 입장해야 합니다.

> **시각화(placeholder)**  
> TODO: 분반 createGroup → leaveRoom → joinRoom(groupId) → endGroup 시퀀스

### 호출 전

* Host·Guest 모두 **메인 룸**에 `joinRoom`한 상태여야 합니다.
* `presence`에서 `createGroup`을 처리할 리스너를 등록합니다.
* 분반에 넣을 `userId` 목록을 준비합니다. (`list` 생략 시 분반 방만 생성됩니다.)

### 유의사항

* Host의 `createGroup` 응답 `groupId`와, Guest가 presence로 받는 `groupId`를 기준으로 이동합니다.
* 분반 입장 후 영상·멤버 UI는 **새 방 기준**으로 다시 publish/subscribe 해야 할 수 있습니다. ([영상 송수신](media.md#영상-송수신-시나리오와-presence))
* `endGroup`는 **메인 룸에서** 호출합니다. 분반 참가자의 메인 복귀(leave → 메인 join)는 앱 정책으로 처리합니다.

### Host (분반 생성·종료)

{% code title="group - host" %}
```javascript
// 메인 룸에 있는 상태에서
const { code, groupId } = await knowledgetalk.createGroup(
  ['kpoint123', 'knowledge123'],
  '분반명'
);
if (code !== '200') return;

// Host 본인도 분반에 들어가려면 Guest와 동일하게 leave → join(groupId)
// (앱 정책에 따라 Host는 메인에 남을 수도 있습니다.)

// 분반 종료는 메인 룸에서
await knowledgetalk.endGroup(groupId);
```
{% endcode %}

### Guest (presence → 방 이동)

{% code title="group - guest (presence)" %}
```javascript
knowledgetalk.addEventListener('presence', async (event) => {
  const msg = event.detail;

  switch (msg.type) {
    case 'createGroup': {
      const mainRoomId = knowledgetalk.getRoomId();
      const { groupId } = msg;

      await knowledgetalk.leaveRoom(mainRoomId);

      const roomData = await knowledgetalk.joinRoom(groupId);
      if (roomData.code !== '200') {
        // 실패 시 메인 복귀 등 앱 정책
        return;
      }

      // 분반에서 미디어·멤버 UI 재구성
      await republishLocalMedia();
      rebuildMemberVideos(roomData.members);
      break;
    }
  }
});
```
{% endcode %}

* 타입 상세: [createGroup](event.md#type-creategroup)
* 입·퇴장 presence: [입장·퇴장 시나리오](room.md#입장퇴장-시나리오와-presence)

