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

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>요청할 roomId 또는 자동생성</td><td>'K43254033'</td></tr><tr><td>title</td><td>방 제목</td><td>'p2pRoom'</td></tr><tr><td>capacity</td><td>수용인원</td><td>2</td></tr><tr><td>destroy</td><td>방 인원 없을 경우 방 종료 // 기본값: true</td><td>true</td></tr></tbody></table>

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

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>roomId</td><td>요청할 roomId 또는 자동생성</td><td>'K43254033'</td></tr><tr><td>title</td><td>방 제목</td><td>'groupRoom'</td></tr><tr><td>capacity</td><td>수용인원</td><td>16</td></tr><tr><td>destroy</td><td>방 인원 없을 경우 방 종료 // 기본값: true</td><td>true</td></tr><tr><td>talkingNoty</td><td>화자 감지 이벤트 // 기본값: false</td><td>false</td></tr></tbody></table>

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

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>id</td><td>유저 아이디</td><td>'kpoint123'</td></tr><tr><td>name</td><td>유저 이름</td><td>'홍길동'</td></tr><tr><td>userType</td><td>host 또는 guest</td><td>'host'</td></tr><tr><td>device</td><td>기기 정보</td><td>'Galaxy Tab'</td></tr><tr><td>video</td><td>비디오 활성화 여부</td><td>true</td></tr><tr><td>audio</td><td>오디오 활성화 여부</td><td>true</td></tr><tr><td>publishing</td><td>stream 배포 여부</td><td>false</td></tr><tr><td>permit</td><td>채팅, 공유등 권한 정보</td><td>{ chat: true, ...}</td></tr></tbody></table>





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





## 방 정보 변경

* **예시**

{% code title="index.js" %}
```javascript
// 방 정보 변경(roomId, title, capacity, host)
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



