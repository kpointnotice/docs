# 분반 기능

> **시각화(placeholder)**  
> TODO: 분반 createGroup → leaveRoom → joinRoom(groupId) 시퀀스

## 분반 시작

### 호출 전

* 메인 룸에 `joinRoom`으로 입장한 상태여야 합니다. (`createGroup`은 현재 `roomId` 기준으로 동작합니다.)
* 분반에 넣을 사용자 `userId` 목록(`list`)을 준비합니다. (방만 만들 경우 `list` 생략 가능)
* 수신측도 `presence` 리스너에서 `createGroup`을 처리할 수 있어야 합니다.

### 유의사항

* `createGroup`은 분반 방을 생성하고(및 list에 이벤트를 보냅니다). **수신자를 자동으로 이동시키지 않습니다.**
* `list`를 생략하면 분반 방만 생성됩니다.
* 분반 참여 후 영상·채팅 등은 새 방 기준으로 다시 연결해야 할 수 있습니다.

### 호출 후

* 응답의 `groupId`를 보관합니다.
* `list`에 포함된 유저는 [createGroup 이벤트](event.md#type-creategroup)를 받은 뒤:
  1. 기존 방에서 [leaveRoom](room.md#undefined-2)
  2. `groupId`로 [joinRoom](room.md#undefined-1)
  3. 필요 시 카메라 publish / subscribe 등 미디어를 다시 연결

### API

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

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>list</td><td><ul><li>분반에 참여할 사용자들</li><li>list 유저들에게 <a href="event.md#type-creategroup">createGroup 이벤트 메시지</a> 보냄<br>메시지 받으면 사용자는 기존 방에서 <a href="room.md#undefined-2">leaveRoom</a> 한 뒤 분반 아이디로 <a href="room.md#undefined-1">joinRoom</a> 해 분반에 참여</li><li>생략 시 분반 방만 생성</li></ul></td><td>['kpoint123', 'knowledge123']</td></tr><tr><td>title</td><td>방 제목</td><td>'분반명'</td></tr></tbody></table>

* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>groupId</td><td>분반 방 아이디</td><td>'r1196417'</td></tr></tbody></table>

---

## 분반 종료

### 호출 전

* **메인 룸**에서 호출합니다. (분반 안에서 호출하는 API가 아닙니다.)
* 종료할 `groupId`를 알고 있어야 합니다.

### 유의사항

* 분반 방을 destroy합니다. 분반에 남아 있는 참가자의 leave/메인 복귀 UI는 앱에서 정의합니다.

### 호출 후

* 분반 참가자를 메인 룸으로 되돌리는 흐름(leave → 메인 join 등)을 앱에서 처리합니다.

### API

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

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>groupId</td><td><ul><li>메인 룸에서 호출</li><li>분반 destroy</li></ul></td><td>'r1196417'</td></tr></tbody></table>

* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

---

## 상대 이벤트 수신 시 (presence)

분반은 `createGroup` API만 호출해서 끝나지 않습니다. **list에 포함된 상대는 presence로 알림을 받은 뒤**, 앱에서 방을 직접 옮겨야 합니다.

| type | 언제 | 앱에서 할 일 예시 |
| ---- | ---- | ----------------- |
| `createGroup` | 호스트가 분반을 만들고 list에 나를 포함 | `leaveRoom` → `joinRoom(groupId)` → (필요 시) 미디어 재연결 |

{% code title="presence - createGroup" %}
```javascript
knowledgetalk.addEventListener('presence', async (event) => {
  const msg = event.detail;

  switch (msg.type) {
    case 'createGroup': {
      const mainRoomId = knowledgetalk.getRoomId();
      const { groupId } = msg;

      // 1) 메인 룸 퇴장
      await knowledgetalk.leaveRoom(mainRoomId);

      // 2) 분반 방 입장
      const roomData = await knowledgetalk.joinRoom(groupId);
      if (roomData.code !== '200') {
        // 실패 시 메인 룸 복귀 등 앱 정책에 따라 처리
        return;
      }

      // 3) 분반에서 영상·UI 다시 구성 (publish / subscribe 등)
      await republishLocalMedia();
      rebuildMemberVideos(roomData.members);
      break;
    }
  }
});
```
{% endcode %}

* 타입 상세: [type: 'createGroup'](event.md#type-creategroup)
* join / leave 자체의 presence 처리는 [방 관련 기능](room.md) 시나리오(가이드 2)를 참고하세요.
