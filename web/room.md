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





## 방 퇴장

{% code title="index.js" %}
```javascript
// 방 퇴장(roomId)
await knowledgetalk.leaveRoom('K43254033');
```
{% endcode %}

* **요청**

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|     roomId    |  String  |       Y      |   퇴장하려는 roomId  |  K43254033  |

*   **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))

## 방 종료

{% code title="index.js" %}
```javascript
// 방 종료(roomId)
await knowledgetalk.destroyRoom('K43254033');
```
{% endcode %}

* **요청**

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|     roomId    |  String  |       Y      |   종료하려는 roomId  |  K43254033  |

*   **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))

## 방에 접속한 유저 조회

{% code title="index.js" %}
```javascript
// 방에 접속한 유저 조회(roomId)
await knowledgetalk.memberList(roomId);
```
{% endcode %}

* **요청**

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|     roomId    |  String  |       Y      |      roomId     |  K43254033  |

*   **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))

| **Parameter** | **Type** | **Required** |  **Description**  |           **Example**          |
| :-----------: | :------: | :----------: | :---------------: | :----------------------------: |
|    members    |  Object  |       Y      | 현재 방에 접속한 members | "kpoint123": { "name": "홍길동" } |

## 권한 부여

{% code title="index.js" %}
```javascript
// 권한 부여(userId, chat, draw, screen, whiteboard, document)
await knowledgetalk.permit('kpoint123', true, true, true, true, true);
```
{% endcode %}

*   **요청**

    <mark style="color:red;">**chat / draw / screen / whiteboard / document 중 하나는 필수**</mark>

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|     target    |  String  |       Y      |    상대 userId    |  kpoint123  |
|      chat     |  Boolean |       N      |      채팅 권한      |     true    |
|      draw     |  Boolean |       N      |      그리기 권한     |     true    |
|     screen    |  Boolean |       N      |     화면공유 권한     |     true    |
|   whiteboard  |  Boolean |       N      |     화이트보드 권한    |     true    |
|    document   |  Boolean |       N      |     자료공유 권한     |     true    |

*   **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))

## 알림 메시지 전송

{% code title="index.js" %}
```javascript
// 알림 메시지 전송(message, target, roomId)
await knowledgetalk.inform('Hello!', 'kpoint123', 'K43254033');
```
{% endcode %}

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|    message    |  String  |       Y      |     전달할 메시지     |    Hello!   |
|     target    |  String  |       N      | 메시지를 전달할 userId |  kpoint123  |
|     roomId    |  String  |       N      | 메시지를 전달할 roomId |  K43254033  |

*   **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))

## 강제 퇴장 요청 메시지 전송

{% code title="index.js" %}
```javascript
// 강퇴 메시지 전송(target)
await knowledgetalk.kickOut('kpoint123');
```
{% endcode %}

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|     target    |  String  |       N      | 메시지를 전달할 userId |  kpoint123  |

*   **응답**

    성공 혹은 실패 시에는 응답 코드를 리턴합니다. ([응답 코드 바로가기](code.md))

## 방 정보 변경

{% code title="index.js" %}
```javascript
// 방 정보 변경(roomId, title, capacity, host)
await knowledgetalk.editRoomInfo('K43254033', 'room title');
```
{% endcode %}

* **요청**

| **Parameter** | **Type** | **Required** | **Description** | **Example** |
| :-----------: | :------: | :----------: | :-------------: | :---------: |
|     roomId    |  String  |       Y      |      roomId     |  K43254033  |
|     title     |  String  |       N      |       방 제목      |   chatRoom  |
|    capacity   |  number  |       N      |       수용인원      |      16     |
|      host     |  String  |       N      |     호스트 아이디     |     k123    |

*   **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))
