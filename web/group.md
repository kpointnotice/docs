# 분반 기능

> **시각화(placeholder)**  
> TODO: 분반 createGroup → leaveRoom → joinRoom(groupId) 시퀀스

## 분반 시작

### 호출 전

- 메인 룸에 `joinRoom`으로 입장한 상태여야 합니다. (`createGroup`은 현재 `roomId` 기준으로 동작합니다.)
- 분반에 넣을 사용자 `userId` 목록(`list`)을 준비합니다. (방만 만들 경우 `list` 생략 가능)
- 수신측도 `presence` 리스너에서 `createGroup`을 처리할 수 있어야 합니다.

### 유의사항

- `createGroup`은 분반 방을 생성하고(및 list에 이벤트를 보냅니다). **수신자를 자동으로 이동시키지 않습니다.**
- `list`를 생략하면 분반 방만 생성됩니다.
- 분반 참여 후 영상·채팅 등은 새 방 기준으로 다시 연결해야 할 수 있습니다.

### 호출 후

- 응답의 `groupId`를 보관합니다.
- `list`에 포함된 유저는 [createGroup 이벤트](event.md#type-creategroup)를 받은 뒤:
  1. 기존 방에서 [leaveRoom](room.md#undefined-2)
  2. `groupId`로 [joinRoom](room.md#undefined-1)
  3. 필요 시 카메라 publish / subscribe 등 미디어를 다시 연결

### API

- **예시**

{% code title="index.js" %}

```javascript
await knowledgetalk.createGroup(["kpoint123", "knowledge123"], "분반명");
```

{% endcode %}

- **타입**

```typescript
createGroup(
    list?: string[];
    title?: string;
): Promise<{
    groupId: string;
    code: ResponseCode;
}>
```

- **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>list</td><td><ul><li>분반에 참여할 사용자들</li><li>list 유저들에게 <a href="event.md#type-creategroup">createGroup 이벤트 메시지</a> 보냄<br>메시지 받으면 사용자는 기존 방에서 <a href="room.md#undefined-2">leaveRoom</a> 한 뒤 분반 아이디로 <a href="room.md#undefined-1">joinRoom</a> 해 분반에 참여</li><li>생략 시 분반 방만 생성</li></ul></td><td>['kpoint123', 'knowledge123']</td></tr><tr><td>title</td><td>방 제목</td><td>'분반명'</td></tr></tbody></table>

- **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>groupId</td><td>분반 방 아이디</td><td>'r1196417'</td></tr></tbody></table>

---

## 분반 종료

### 호출 전

- **메인 룸**에서 호출합니다. (분반 안에서 호출하는 API가 아닙니다.)
- 종료할 `groupId`를 알고 있어야 합니다.

### 유의사항

- **메인 룸**에서 호출해야 합니다. 분반 안에서 호출하면 실패할 수 있습니다.
- 분반 방(미디어·방 정보)을 destroy합니다. 분반에 **남아 있는 Guest에게는 종료 presence(`Event`)가 가지 않습니다.**
- 잔류 Guest는 영상이 끊기고 SDK `roomId`는 분반 ID로 남을 수 있습니다. 메인 복귀(`leaveRoom` → 메인 `joinRoom`)는 **앱에서 반드시 처리**해야 합니다.

### 호출 후

- 호출한 Host만 `endGroup` 응답(`code`)을 받습니다.
- Guest 복귀를 위해 Host가 `inform`으로 종료를 알리거나, Guest가 미디어/시그널 실패를 감지한 뒤 메인으로 돌아가게 합니다.

### API

- **예시**

{% code title="index.js" %}

```javascript
await knowledgetalk.endGroup(groupId);
```

{% endcode %}

- **타입**

```typescript
endGroup(
    groupId: string;
): Promise<{
    code: ResponseCode;
}>
```

- **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>groupId</td><td><ul><li>메인 룸에서 호출</li><li>분반 destroy</li></ul></td><td>'r1196417'</td></tr></tbody></table>

- **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

---

## 시나리오: 분반 이동 (생성 → 입장 → 종료)

`createGroup`만으로 참가자가 자동 이동하지 않습니다. **list에 포함된 클라이언트는 presence를 받은 뒤** 메인 룸을 나와 분반 `groupId`로 다시 입장해야 합니다.

> **시각화(placeholder)**  
> TODO: 분반 createGroup → leaveRoom → joinRoom(groupId) → endGroup 시퀀스

### 호출 전

- Host·Guest 모두 **메인 룸**에 `joinRoom`한 상태여야 합니다.
- `presence`에서 `createGroup`을 처리할 리스너를 등록합니다.
- 분반에 넣을 `userId` 목록을 준비합니다. (`list` 생략 시 분반 방만 생성됩니다.)

### 유의사항

- Host의 `createGroup` 응답 `groupId`와, Guest가 presence로 받는 `groupId`를 기준으로 이동합니다.
- 분반 입장 후 영상·멤버 UI는 **새 방 기준**으로 다시 publish/subscribe 해야 할 수 있습니다. ([영상 송수신](media.md#영상-송수신-시나리오와-presence))
- `endGroup`는 **메인 룸에서** 호출합니다. 분반에 남은 Guest에게는 Event가 가지 않으므로, `inform` 등으로 알린 뒤 Guest가 `leaveRoom` → 메인 `joinRoom` 하도록 **앱에서 복귀를 처리**해야 합니다.

### Host (분반 생성·종료)

{% code title="group - host" %}

```javascript
// 메인 룸에 있는 상태에서
const { code, groupId } = await knowledgetalk.createGroup(
  ["kpoint123", "knowledge123"],
  "분반명",
);
if (code !== "200") return;

// Host 본인도 분반에 들어가려면 Guest와 동일하게 leave → join(groupId)
// (앱 정책에 따라 Host는 메인에 남을 수도 있습니다.)

// 분반 종료는 메인 룸에서. 분반 잔류 Guest에게는 endGroup Event가 없으므로
// 분반에 있는 userId로 inform 한 뒤 endGroup
const mainRoomId = knowledgetalk.getRoomId();
for (const guestId of breakoutMemberIds) {
  await knowledgetalk.inform(
    { type: "endGroup", groupId, mainRoomId },
    guestId
  );
}
await knowledgetalk.endGroup(groupId);
```

{% endcode %}

### Guest (presence → 방 이동)

{% code title="group - guest (presence)" %}

```javascript
knowledgetalk.addEventListener("presence", async (event) => {
  const msg = event.detail;

  switch (msg.type) {
    case "createGroup": {
      const mainRoomId = knowledgetalk.getRoomId();
      const { groupId } = msg;

      // 1) 메인 룸 퇴장
      await knowledgetalk.leaveRoom(mainRoomId);

      // 2) 분반 방 입장
      const roomData = await knowledgetalk.joinRoom(groupId);
      if (roomData.code !== "200") {
        // 실패 시 메인 룸 복귀 등 앱 정책에 따라 처리
        return;
      }

      // 3) 분반에서 영상·UI 다시 구성 (publish / subscribe 등)
      await republishLocalMedia();
      rebuildMemberVideos(roomData.members);
      break;
    }

    case "inform": {
      // endGroup presence는 없음. Host inform으로 종료를 알린 경우
      if (msg.message?.type !== "endGroup") break;
      const groupRoomId = knowledgetalk.getRoomId();
      await knowledgetalk.leaveRoom(groupRoomId);
      await knowledgetalk.joinRoom(msg.message.mainRoomId);
      break;
    }
  }
});
```

{% endcode %}

- 타입 상세: [type: 'createGroup'](event.md#type-creategroup), [inform](event.md#type-inform)
- 입·퇴장 presence: [입장·퇴장 시나리오](room.md#입장퇴장-시나리오와-presence)
