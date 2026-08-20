# 이벤트 메시지

## 이벤트 메시지

다른 참여자들의 입장, 퇴장 등 상태 등 클라이언트에서 서버로부터 오는 이벤트 메시지들에 대한 설명

### 이벤트 메시지 알림

{% code title="index.js" %}

```javascript
// 이벤트 메시지 알림
knowledgetalk.addEventListener("presence", async event => {
    const { type, ...data } = e.detail;

    console.log("이벤트 타입", type);
    console.log("이벤트 데이터", data);

    // 타입별 분기
    switch (type) {
        case "join": {
            break;
        }
    }
}
```

{% endcode %}

## 타입별 상세 메시지 예시

## type: "join"

다른 사용자의 입장 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "join";
  roomId: string;
  user: Member;
}
```

- [Member 참조](room.md#undefined-1)

## type: "leave"

다른 사용자의 퇴장 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "leave";
  roomId: string;
  user: string;
}
```

## type: "publish"

미디어 서버에서 수신 가능한 사용자들의 영상 알림

<mark style="color:red;">publishVideo 호출 시 type === "cam", screenStart(그룹) 호출 시 type === "screen" 으로 분기해 처리</mark>

그룹 화면 공유의 **실제 영상 수신**은 이 이벤트에서 `subscribeVideo(feed.id, "screen")`로 처리합니다. `screen` 이벤트만으로는 스트림이 연결되지 않습니다. ([공유 기능](share.md#화면-공유-통합-흐름), [그룹 샘플](../sample/group.md#6-화면-공유))

- **타입**

```typescript
{
      eventOp: "presence";
      type: "publish";
      roomId: string;
      feeds: Feed[];
}

// publishVideo로부터 송신된 메시지
type Feed = Member & { type: "cam" };

// screenStart로부터 송신된 메시지
type Feed = {
      id: string;
      type: "screen";
};
```

- [Member 참조](room.md#undefined-1)

- **feeds 사용 예시**\
  [subscribeVideo](media.md#undefined-1)를 호출해 stream을 수신합니다.

```typescript
case "publish": {
  data.feeds.forEach(async (feed) => {
    const stream = await knowledgetalk.subscribeVideo(feed.id, feed.type);

    if (feed.type === "cam") {
      // ... 유저 캠 stream 처리
    }

    if (feed.type === "screen") {
      // ... 화면 공유 stream 처리
    }
  });

  break;
};
```

## type: "subscribed"

해당 사용자의 영상에 대한 P2P 연결 완료 알림

<mark style="color:red;">cam: true인 경우 publishP2P로부터 송신된 메시지</mark>

<mark style="color:red;">cam: false인 경우 screenStart로부터 송신된 메시지</mark>

- **타입**

```typescript
{
  eventOp: "presence";
  type: "subscribed";
  user: string;
  cam: boolean;
}
```

- **p2p stream 조회 예시**

```typescript
case "subscribed": {
  const { cam, user } = data;

  if (cam) {
    const stream = knowledgetalk.getStream(user);
    // ... 유저 캠 stream 처리
  } else {
    const stream = knowledgetalk.getStream("screen");
    // ... 화면 공유 stream 처리
  }

  break;
};
```

## type: "screen"

화면 공유 알림, screenStart 호출 시 발생

- P2P의 경우 subscribed 이벤트와 screen 이벤트가 동시에 발생합니다.\
  ["p2p stream 조회 예시"](event.md#type-subscribed)와 같이 처리한다면 screen에서는 따로 처리하지 않아도 됩니다.
- 그룹의 경우 publish 이벤트와 screen 이벤트가 동시에 발생하므로 \
  ["feeds 사용 예시"](event.md#type-publish)와 같이 처리한다면 screen에서는 따로 처리하지 않아도 됩니다.
- 송수신 시나리오: [화면 공유 송수신](share.md#시나리오-화면-공유-송수신)

- **타입**

```typescript
{
  eventOp: "presence";
  type: "screen";
  roomId: string;
  user: string;
}
```

## type: "whiteBoard"

화이트보드 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "whiteboard";
  roomId: string;
  user: string;
}
```

## type: "document"

자료 공유 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "document";
  roomId: string;
  user: string;
}
```

## type: "documentShare"

이미지 경로 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "documentShare";
  roomId: string;
  user: string;
  img: string; // img url
}
```

<<<<<<< HEAD
## type: "shareStop"
=======


## type: 'reqCanvasImage'

다른 사용자가 `reqCanvasImage()`를 호출하여 현재 캔버스 이미지의 전송을 요청했음을 알립니다.

SDK는 이 이벤트를 수신하면 `canvasInit()`으로 등록한 캔버스를 PNG 이미지로 변환하고, 요청자에게 자동으로 전송합니다. 이벤트는 자동 응답 처리 후 `presence` 이벤트 리스너에도 전달됩니다.

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'reqCanvasImage';
      sender: string; // 캔버스 이미지를 요청한 사용자 ID
      roomId: string;
}
```



## type: 'updateImage'

`reqCanvasImage()`로 요청한 캔버스 이미지를 수신했음을 알립니다.

SDK는 이 이벤트를 수신하면 `img` 이미지를 `canvasInit()`으로 등록한 캔버스에 자동으로 반영합니다. 이미지 반영을 시작한 후 이벤트는 `presence` 이벤트 리스너에도 전달됩니다.

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'updateImage';
      sender: string; // 캔버스 이미지를 전송한 사용자 ID
      img: string; // PNG 형식의 Data URL
}
```



## type: 'shareStop'
>>>>>>> guide/4-canvas-sync-events

공유 중지 알림

- 송수신 시나리오: [화면 공유 송수신](share.md#시나리오-화면-공유-송수신)

- **타입**

```typescript
{
  eventOp: "presence";
  type: "shareStop";
  roomId: string;
  user: string;
}
```

## type: "chat"

채팅 메시지 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "chat";
  user: string;
  message: string;
}
```

## type: "inform"

커스텀 메시지 수신 알림\
정의되지 않은 메시지가 필요할 경우 사용할 수 있습니다.

- P2P 재연결처럼 앱 규약 객체(`{ type: "reconnect" }` 등)를 `message`로 넘기는 응용 예시는 [media · P2P 재연결](media.md#p2p-응용-시나리오-재연결)을 참고합니다.

- **타입**

```typescript
{
  eventOp: "presence";
  type: "inform";
  user: string;
  message: any;
}
```

## type: "editUserInfo"

사용자 정보 변경 알림

- 송신 측이 `editUserInfo(..., broadcast: true)`일 때만 수신됩니다. `broadcast: false`면 이 presence가 오지 않아 상대방 UI를 갱신할 수 없습니다. ([broadcast 설명](userInfo.md#사용자-정보-변경))
- `video` / `audio` 값으로 상대방 화면·마이크 UI를 갱신합니다. 본인 비디오 숨김 시나리오는 [userInfo](userInfo.md#시나리오-본인-비디오-숨김)를 참고합니다.

- **타입**

```typescript
{
  eventOp: "presence";
  type: "editUserInfo";
  user: string;
  name: string;
  video: boolean;
  audio: boolean;
}
```

## type: "createGroup"

분반 생성 알림

수신 후 앱에서 `leaveRoom` → `joinRoom(groupId)`로 분반에 참여해야 합니다. SDK가 자동으로 방을 바꿔 주지 않습니다. ([분반 기능 - 호출 후](group.md#호출-후), [분반 이동 시나리오](group.md#시나리오-분반-이동-생성--입장--종료))

`endGroup`에는 대응하는 presence 타입이 없습니다. 분반에 남은 Guest 복귀는 [분반 종료](group.md#분반-종료)처럼 앱에서 처리합니다.

- **타입**

```typescript
{
  eventOp: "presence";
  type: "createGroup";
  user: string;
  groupId: string;
}
```

## type: "kickOut"

강제 퇴장 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "kickOut";
  user: string;
  roomId: string;
}
```

## type: "talking"

화자 감지 알림

- **타입**

```typescript
{
  eventOp: "presence";
  type: "talking";
  user: string;
  roomId: string;
  talking: boolean;
}
```

- 현재 미사용 중인 메서드

#### ~~type: "drawingClassStart"~~

{% code title="event message sample" %}

```json
// 미술수업시작 알림
{
  "eventOp": "presence",
  "type": "drawingClassStart",
  "user": "kpoint123",
  "roomId": "K43254033"
}
```

{% endcode %}

#### ~~type: "drawingShareStart"~~

{% code title="event message sample" %}

```json
// 그리기공유알림 알림
{
  "eventOp": "presence",
  "type": "drawingShare",
  "user": "kpoint123",
  "roomId": "K43254033"
}
```

{% endcode %}

#### ~~type: "drawingShareStop"~~

{% code title="event message sample" %}

```json
// 그리기공유종료 알림
{
  "eventOp": "presence",
  "type": "drawingShareStop",
  "user": "kpoint123",
  "roomId": "K43254033"
}
```

{% endcode %}

#### ~~type: "drawingShareImg"~~

{% code title="event message sample" %}

```json
// 그리기종료 후 이미지 전송
{
  "eventOp": "presence",
  "type": "drawingShareImg",
  "user": "kpoint123",
  "roomId": "K43254033",
  "img": "img data..."
}
```

{% endcode %}

#### ~~type: "drawingClassStop"~~

{% code title="event message sample" %}

```json
// 미술수업종료 알림
{
  "eventOp": "presence",
  "type": "drawingClassStop",
  "user": "kpoint123",
  "roomId": "K43254033"
}
```

{% endcode %}
