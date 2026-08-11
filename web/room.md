# 방 관련 기능

## P2P 방 생성

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.createRoom('K43254033', 'p2pRoom', 2);
```
{% endcode %}



* **타입**

```typescript
createRoom(
    roomId?: string;
    title?: string;
    capacity?: number;
    destroy?: boolean;
): Promise<{
    code: ResponseCode;
    roomId: string;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>요청할 roomId 또는 자동생성</td><td>'K43254033'</td></tr><tr><td>title</td><td>방 제목</td><td>'p2pRoom'</td></tr><tr><td>capacity</td><td>수용인원</td><td>2</td></tr><tr><td>destroy</td><td><ul><li>방 인원 없을 경우 방 종료</li><li>기본값: true</li></ul></td><td>true</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>roomId</td><td>랜덤 또는 요청된 roomId</td><td>'K43254033'</td></tr></tbody></table>





## 그룹통화 방 생성

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.createVideoRoom('K43254033', 'groupRoom', 16);
```
{% endcode %}



* **타입**

```typescript
createVideoRoom(
    roomId?: string;
    title?: string;
    capacity?: string;
    destroy?: boolean;
    talkingNoty?: boolean;
): Promise<{
    code: ResponseCode;
    roomId: string;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>요청할 roomId 또는 자동생성</td><td>'K43254033'</td></tr><tr><td>title</td><td>방 제목</td><td>'groupRoom'</td></tr><tr><td>capacity</td><td>수용인원</td><td>16</td></tr><tr><td>destroy</td><td><ul><li>방 인원 없을 경우 방 종료</li><li>기본값: true</li></ul></td><td>true</td></tr><tr><td>talkingNoty</td><td><ul><li>화자 감지 이벤트</li><li>기본값: false</li></ul></td><td>false</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>roomId</td><td>랜덤 또는 요청된 roomId</td><td>'K43254033'</td></tr></tbody></table>





## 방 입장

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.joinRoom('K43254033');
```
{% endcode %}



* **타입**

```typescript
joinRoom(
    roomId: string;
): Promise<{
    code: ResponseCode;
    createdAt: string;
    fileServerUrl: string;
    isRecording: boolean;
    media: boolean;
    roomId: string;
    talkingNoty: boolean;
    title: string;
    host: Member;
    members: {
        [userId: string]: Member;
    }
}>
```

```typescript
type Member = {
    id: string;
    name: string;
    userType: 'host' | 'guest';
    device: string;
    video: boolean;
    audio: boolean;
    pulishing: boolean;
    permit: {
        screen: boolean;
        chat: boolean;
        whiteboard: boolean;
        draw: boolean;
        document: boolean;
    }
}
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>랜덤 또는 요청된 roomId</td><td>'K43254033'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>createdAt</td><td>방 생성 일시</td><td>'2024/05/30 13:38:37'</td></tr><tr><td>fileServerUrl</td><td>파일 서버 주소</td><td>'https://fileServer'</td></tr><tr><td>isRecording</td><td>현재 녹화 여부</td><td>false</td></tr><tr><td>media</td><td>미디어 서버 사용 여부</td><td>false</td></tr><tr><td>roomId</td><td>방 아이디</td><td>'K43254033'</td></tr><tr><td>talkingNoty</td><td>화자 감지 활성화 여부</td><td>false</td></tr><tr><td>title</td><td>방 제목</td><td>'테스트방'</td></tr><tr><td>host</td><td>방 host 정보</td><td>Member</td></tr><tr><td>members</td><td>현재 방에 접속한 유저 정보</td><td>Members</td></tr></tbody></table>



* **Member**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>id</td><td>유저 아이디</td><td>'kpoint123'</td></tr><tr><td>name</td><td>유저 이름</td><td>'홍길동'</td></tr><tr><td>userType</td><td>host 또는 guest</td><td>'host'</td></tr><tr><td>device</td><td>기기 정보</td><td>'Galaxy Tab'</td></tr><tr><td>video</td><td>비디오 활성화 여부</td><td>true</td></tr><tr><td>audio</td><td>오디오 활성화 여부</td><td>true</td></tr><tr><td>publishing</td><td>영상 송신여부</td><td>false</td></tr><tr><td>permit</td><td>채팅, 공유등 권한 정보</td><td>{ chat: true, ...}</td></tr></tbody></table>

* 기존에 방에 참여중인 유저는[ join 이벤트 메시지](event.md#type-join)로 멤버 정보 수신





## 방 퇴장

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.leaveRoom('K43254033');
```
{% endcode %}



* **타입**

```typescript
leaveRoom(
    roomId: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>퇴장할 방 아이디</td><td>'K43254033'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* leaveRoom 호출 시 방에 [leave 이벤트 메시지](event.md#type-leave) 보냄





## 방 종료

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.destroyRoom('K43254033');
```
{% endcode %}



* **타입**

```typescript
destroyRoom(
    roomId: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>종료할 방 아이디</td><td>'K43254033'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>





## 방에 접속한 유저 조회

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.memberList(roomId);
```
{% endcode %}



* **타입**\
  [Member 타입 참조](room.md#undefined-1)

```typescript
memberList(
    roomId: string;
): Promise<{
    [userId: string]: Member;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>조회할 방 아이디</td><td>'200'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr><tr><td>members</td><td>현재 방에 접속한 유저 정보</td><td>Members</td></tr></tbody></table>





## 권한 부여

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.permit('kpoint123', true, true, true, true, true);
```
{% endcode %}



* **타입**

```typescript
permit(
    target: string;
    chat?: boolean;
    draw?: boolean;
    screen?: boolean;
    whiteboard?: boolean;
    document?: boolean;
): Promise<{
    code: ResponseCode;
}>
```



*   **요청 상세**

    <mark style="color:red;">**chat / draw / screen / whiteboard / document 중 하나는 필수**</mark>

| Parameter  | Description  | Example     |
| ---------- | ------------ | ----------- |
| target     | 타겟 아이디       | 'kpoint123' |
| chat       | 채팅 권한        | true        |
| draw       | 그리기 권한       | false       |
| screen     | 화면 공유 권한     | false       |
| whiteboard | 화이트 보드 공유 권한 | false       |
| document   | 자료 공유 권한     | false       |



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>





## 알림 메시지 전송

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.inform('Hello!', 'kpoint123', 'K43254033');
```
{% endcode %}



* **타입**

```typescript
inform(
    message: any;
    target?: string;
    roomId?: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>message</td><td>전달할 메시지</td><td>'Hello!'</td></tr><tr><td>target</td><td>메시지를 전달할 유저 아이디</td><td>'kpoint123'</td></tr><tr><td>roomId</td><td>메시지를 전달할 방 아이디</td><td>'K43254033'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* 타겟유저는 [inform 이벤트 메시지](event.md#type-inform)를 받아 사용
* `message`는 문자열뿐 아니라 객체도 가능합니다. P2P 재연결 등 응용 예시는 [media · P2P 재연결](media.md#p2p-응용-시나리오-재연결)을 참고합니다.





## 강제 퇴장 요청 메시지 전송

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.kickOut('kpoint123');
```
{% endcode %}



* **타입**

```typescript
kickOut(
    target: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>target</td><td>메시지를 전달할 userId</td><td>'kpoint123'</td></tr></tbody></table>



* **요청 응답**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* target 유저는 [kickOut 이벤트 메시지](event.md#type-kickout)를 수신해서 leaveRoom 진행





## 방 정보 변경

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.editRoomInfo('K43254033', 'room title');
```
{% endcode %}



* **타입**

```typescript
editRoomInfo(
    roomId: string;
    title?: string;
    capacity?: number;
    host?: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>방 아이디</td><td>'K43254033'</td></tr><tr><td>title</td><td>방 제목</td><td>'chatRoom'</td></tr><tr><td>capacity</td><td>수용인원</td><td>16</td></tr><tr><td>host</td><td>호스트 아이디</td><td>'k123'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

---

## 입장·퇴장 시나리오와 presence

`joinRoom` / `leaveRoom`은 요청-응답만으로 끝나지 않습니다. **이미 방에 있는 다른 클라이언트**는 presence로 입·퇴장을 알게 되고, 여기서 video 박스·멤버 목록을 갱신해야 합니다.

> **시각화(placeholder)**  
> TODO: joinRoom / leaveRoom ↔ presence join·leave 시퀀스

### 호출 전 (공통)

* `init`을 완료합니다.
* `knowledgetalk.addEventListener('presence', ...)`를 등록합니다. (입장 전에 등록하는 것을 권장합니다.)
* 상대방 video/멤버 UI를 만들·지울 헬퍼(`createVideoBox`, `removeVideoBox` 등)를 준비합니다.

### 유의사항

* `joinRoom` 응답의 `members`는 **현재 이미 있는 사람**입니다. 그 이후 들어오는 사람은 `join` presence로만 알 수 있습니다.
* 상대방이 `leaveRoom`하면 본인에게 `leave` presence가 옵니다. DOM만 지우면 스트림/리스너가 남을 수 있으므로, 앱에서 정리 정책을 정해야 합니다.
* `kickOut`을 받은 대상은 presence 후 스스로 `leaveRoom`을 호출하는 흐름이 일반적입니다.

### 상대방 이벤트 수신 시 (presence)

| type | 언제 | 앱에서 할 일 예시 |
| ---- | ---- | ----------------- |
| `join` | 다른 사용자가 방에 입장 | 멤버 목록 추가, 카메라용 video 박스 생성 |
| `leave` | 다른 사용자가 퇴장 | video 박스 제거, (화면 공유 중이면) screen DOM도 제거 |
| `kickOut` | 강제 퇴장 요청을 받음 | `leaveRoom` 호출 후 로비/대기 화면으로 이동 |

{% code title="presence - join / leave / kickOut" %}
```javascript
knowledgetalk.addEventListener('presence', async (event) => {
  const msg = event.detail;

  switch (msg.type) {
    case 'join': {
      // msg.user: Member (id, name, ...)
      const userId = msg.user.id ?? msg.user.userId;
      createVideoBox(userId);
      // 그룹에서 상대방이 이미 publish 중이면 이후 publish 이벤트로 subscribe
      break;
    }

    case 'leave': {
      // msg.user: 퇴장한 userId (string)
      removeVideoBox(msg.user);
      removeScreenVideoBox?.(msg.user);
      break;
    }

    case 'kickOut': {
      const roomId = knowledgetalk.getRoomId();
      await knowledgetalk.leaveRoom(roomId);
      // 로컬 스트림·UI 정리 후 대기 화면으로
      cleanupLocalSession();
      break;
    }
  }
});
```
{% endcode %}

* 타입 상세: [join](event.md#type-join), [leave](event.md#type-leave), [kickOut](event.md#type-kickout)
* 샘플 흐름: [P2P 샘플](../sample/p2p.md), [그룹 샘플](../sample/group.md)

