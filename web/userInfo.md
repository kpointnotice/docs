# 사용자 정보 관련 기능

## 사용자 정보 변경

이름·비디오·오디오 상태를 바꾸고, 필요하면 방 참가자에게 `editUserInfo` presence로 알립니다.

### 호출 전

- `init` 및 방 입장(`joinRoom`)이 끝난 상태여야 합니다.
- P2P에서 video/audio track을 바꿀 때는 `target`에 상대방 userId를 넘깁니다.
- **다른 참가자 UI에 반영하려면 `broadcast`를 `true`로 두고** `presence` `editUserInfo` 핸들러를 등록해야 합니다.

### 유의사항

- `name` / `video` / `audio` 중 **하나는 필수**입니다. 바꾸지 않을 인자는 `undefined`(또는 SDK 기본값)로 둡니다.
- `video`/`audio`를 바꾸면 SDK가 **호출한 클라이언트 쪽** 로컬(및 P2P `target` 스트림) track `enabled`를 먼저 갱신합니다. 이 로컬 적용은 `broadcast`와 무관합니다.
- **`broadcast` (중요)**
  - `true`(기본값): 서버가 방(또는 `target`)의 다른 유저에게 [editUserInfo presence](event.md#type-edituserinfo)를 보냅니다. 상대방 앱이 닉네임·카메라·마이크 UI를 바꿀 수 있습니다.
  - `false` 또는 알림이 나가지 않는 호출: **본인 기기 track만** 바뀌고, 방 안 다른 유저는 presence를 받지 못해 UI 상태가 그대로인 것처럼 보입니다. (검은 화면/무음은 미디어 track 쪽 효과일 수 있어도, “카메라 끔” 배지·아이콘 등은 갱신되지 않습니다.)
  - 상대방에게 상태 변경을 보여 줘야 하는 UX(비디오 숨김, 음소거, 닉네임 변경)에서는 **`broadcast: true`를 생략하지 말고 명시**합니다. `false`는 다른 참가자에게 알릴 필요가 없는 내부 동기화용입니다.
  - 인자 순서상 `target`만 넘기려면 네 번째에 `true`를 넣어야 합니다.  
    `editUserInfo(undefined, false, undefined, partnerId)`처럼 네 번째에 userId를 넣으면 `broadcast`로 해석되어 의도와 달라질 수 있습니다.
- 피어를 끊는 API(`removePeer` / `removeLocalPeer`)와 혼동하지 않습니다. 가리기·끄기는 이 API를 사용하고, 재연결·세션 정리는 [media 재연결 시나리오](media.md#p2p-응용-시나리오-재연결)를 사용합니다.

### 호출 후

- 응답 코드로 성공 여부를 확인합니다.
- `broadcast: true`인 경우 상대방은 [editUserInfo 이벤트](event.md#type-edituserinfo)의 `video` / `audio` / `name`으로 UI를 갱신합니다. `false`면 이 이벤트가 가지 않습니다.

### API

- **예시**

{% code title="index.js" %}

```javascript
// broadcast 기본값은 true. 상대방 UI 반영이 필요하면 명시하는 것을 권장
await knowledgetalk.editUserInfo("홍길동", true, false, true);

// P2P: target을 쓰려면 4번째에 broadcast를 넣고 5번째에 userId
await knowledgetalk.editUserInfo(
  undefined,
  false,
  undefined,
  true,
  "kpoint123",
);
```

{% endcode %}

- **타입**

```typescript
editUserInfo(
    name?: string;
    video?: boolean;
    audio?: boolean;
    broadcast?: boolean;
    target?: string;
): Promise<{
    code: ResponseCode;
}>
```

- **요청 상세**\
  <mark style="color:red;">**name / video / audio 중 하나는 필수**</mark>

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>name</td><td>유저 닉네임</td><td>'홍길동'</td></tr><tr><td>video</td><td>비디오 활성화 여부</td><td>true</td></tr><tr><td>audio</td><td>오디오 활성화 여부</td><td>true</td></tr><tr><td>broadcast</td><td><ul><li><b>true (기본·권장)</b>: 다른 참가자에게 <a href="event.md#type-edituserinfo">editUserInfo presence</a>로 변경을 알립니다. 상대방 UI 갱신에 필요합니다.</li><li><b>false</b>: presence를 전송하지 않습니다. 호출자 로컬 track만 변경되어 방 안 다른 유저 UI는 갱신되지 않습니다.</li></ul></td><td>true</td></tr><tr><td>target</td><td>P2P 시 상대방 아이디 (5번째 인자. 쓸 때 broadcast를 4번째로 명시합니다.)</td><td>user1234</td></tr></tbody></table>

- **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

---

## 시나리오: 본인 비디오 숨김

상대방에게 본인 카메라 화면을 **안 보이게** 하려면 피어를 끊지 말고, track enable + 상태 알림 + UI로 처리합니다.

> **시각화(placeholder)**  
> TODO: video on/off UI 흐름

### 올바른 방법

1. `editUserInfo`로 `video: false`를 설정합니다. (P2P면 `target`에 상대방 id를 넣습니다.)
2. **`broadcast: true`를 반드시 명시**해 상대방에게 presence가 가게 합니다. (`false`이거나 인자 순서를 잘못 넘기면 본인만 꺼지고 상대방 UI는 그대로입니다.)
3. 상대방은 `presence` `editUserInfo`에서 `video === false`를 받아 **UI만** 플레이스홀더/가림 처리합니다.
4. 다시 켤 때는 `video: true` + `broadcast: true`로 동일 API를 호출합니다.

{% code title="hide my video" %}

```javascript
// P2P: 상대방에게만 알림 + P2P 로컬 스트림 video track 비활성
await knowledgetalk.editUserInfo(
  undefined,
  false, // video off
  undefined,
  true, // broadcast
  partnerId,
);

// 다시 켜기
await knowledgetalk.editUserInfo(undefined, true, undefined, true, partnerId);

// 그룹(미디어 서버): target 없이 broadcast
await knowledgetalk.editUserInfo(undefined, false, undefined, true);
```

{% endcode %}

### 잘못된 방법

- “안 보여 주려면 `removePeer` / `removeLocalPeer`로 양쪽에 피어를 끊어야 한다” → 이는 **재연결·세션 종료**용입니다. 카메라 끄기/가리기와는 다릅니다.
- `editUserInfo(..., broadcast: false)`만으로 상대방 UI까지 바뀔 것이라 기대하기 → **로컬 track만** 바뀌고 방 안 다른 유저에게는 `editUserInfo` presence가 가지 않습니다.
- 재연결이 필요하면 [P2P 재연결 시나리오](media.md#p2p-응용-시나리오-재연결)를 참고합니다.

### 상대방 이벤트 수신 시 (presence)

{% code title="presence - editUserInfo" %}

```javascript
knowledgetalk.addEventListener("presence", (event) => {
  const msg = event.detail;

  switch (msg.type) {
    case "editUserInfo": {
      const { user, video, audio, name } = msg;

      if (typeof video === "boolean") {
        // peer를 끊지 말고 UI만 가림/복원
        setRemoteVideoVisible(user, video);
      }
      if (typeof audio === "boolean") {
        setRemoteAudioMuted(user, !audio);
      }
      if (name) {
        setRemoteDisplayName(user, name);
      }
      break;
    }
  }
});
```

{% endcode %}

- 타입 상세: [editUserInfo](event.md#type-edituserinfo)
