# 이벤트 메시지

## 이벤트 메시지

다른 참여자들의 입장, 퇴장 등 상태 등 클라이언트에서 서버로 부터 오는 이벤트 메시지들에 대한 설명

### 이벤트 메시지 알림

{% code title="index.js" %}
```javascript
// 이벤트 메시지 알림
knowledgetalk.addEventListener('presence', async event => {
    const { type, ...data } = e.detail;

    console.log('이벤트 타입', type);
    console.log('이벤트 데이터', data);

    // 타입별 분기
    switch(type) {
        case 'join': {
            break;
        }
    }
}
```
{% endcode %}





## 타입별 상세 메시지 예시

## type: 'join'

다른 사용자의 입장 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'join';
      roomId: string;
      user: Member;
}
```

* [Member 참조](room.md#undefined-1)



## type: 'leave'

다른 사용자의 퇴장 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'leave';
      roomId: string;
      user: string;
}
```



## type: 'publish'

미디어 서버에서 수신 가능한 사용자들의 영상 알림

<mark style="color:red;">publishVideo 호출시 type === 'cam' 으로 분기해 처리</mark>

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'publish';
      roomId: string;
      feeds: Feed[];
}

// publishVideo 로 부터 송신된 메시지
type Feed = Member & { type: 'cam' };

// screenStart 로 부터 송신된 메시지
type Feed = { 
      id: string;
      type: 'screen';
};
```

* [Member 참조](room.md#undefined-1)

\


* **feeds 사용 예시**\
  [subscribeVideo](media.md#undefined-1) 를 호출해 stream 수신

```typescript
case 'publish': {
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



## type: 'subscribed'

해당 사용자의 영상에 대한 P2P 연결 완료 알림

<mark style="color:red;">cam: true 인 경우 publishP2P 로 부터 송신된 메시지</mark>

<mark style="color:red;">cam: false 인 경우 screenStart로 부터 송신된 메시지</mark>

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'subscribed';
      user: string;
      cam: boolean;
}
```



* **p2p stream 조회 예시**

```typescript
case 'subscribed': {
  const { cam, user } = data;
  
  if (cam) {
    const stream = knowledgetalk.getStream(user);
    // ... 유저 캠 stream 처리
  } else {
    const stream = knowledgetalk.getStream('screen');
    // ... 화면 공유 stream 처리
  }

  break;
};
```



## type: 'screen'

화면공유 알림, screenStart 호출시 발생

<mark style="color:red;">p2p의 경우 subscribed 이벤트와 screen 이벤트가 동시에 발생하므로</mark> \
["p2p stream 조회 예시"](event.md#type-subscribed) <mark style="color:red;">와 같이 처리한다면 screen에서는 따로 처리하지 않아도 됨</mark>

<mark style="color:red;">group의 경우  publish 이벤트와 screen 이벤트가 동시에 발생하므로</mark> \
["feeds 사용 예시"](event.md#type-publish) <mark style="color:red;">와 같이 처리한다면 screen에서는 따로 처리하지 않아도 됨</mark>

* **타입**&#x20;

```typescript
{
      eventOp: 'presence';
      type: 'screen';
      roomId: string;
      user: string;
}
```



## type: 'whiteBoard'

화이트보드 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'whiteboard';
      roomId: string;
      user: string;
}
```



## type: 'document'

자료공유 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'document';
      roomId: string;
      user: string;
}
```



## type: 'documentShare'

이미지 경로 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'documentShare';
      roomId: string;
      user: string;
      img: string; // img url
}
```



## type: 'shareStop'

공유 중지 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'shareStop';
      roomId: string;
      user: string;
}
```



## type: 'chat'

채팅 메시지 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'chat';
      user: string;
      message: string;
}
```



## type: 'inform'

커스텀  메시지 수신 알림\
정의되지 않은 메시지가 필요 할 경우 사용할 수 있습니다.

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'inform';
      user: string;
      message: any;
}
```



## type: 'editUserInfo'

사용자 정보 변경 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'editUserInfo';
      user: string;
      name: string;
      video: boolean;
      audio: boolean;
}
```



## type: 'createGroup'

분반 생성 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'createGroup';
      user: string;
      groupId: string;
}
```



## type: 'kickOut'

강제 퇴장 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'kickOut';
      user: string;
      roomId: string;
}
```



## type: 'talking'

화자 감지 알림

* **타입**

```typescript
{
      eventOp: 'presence';
      type: 'talking';
      user: string;
      roomId: string;
      talking: boolean;
}
```





* 현재 미사용 중 인 메서드

#### ~~type: 'drawingClassStart'~~

{% code title="event message sample" %}
```json
  // 미술수업시작 알림
  {
      eventOp: 'presence',
      type: 'drawingClassStart',
      user: 'kpoint123',
      roomId: 'K43254033'
  }
```
{% endcode %}

#### ~~type: 'drawingShareStart'~~

{% code title="event message sample" %}
```json
  // 그리기공유알림 알림
  {
      eventOp: 'presence',
      type: 'drawingShare',
      user: 'kpoint123',
      roomId: 'K43254033'
  }
```
{% endcode %}

#### ~~type: 'drawingShareStop'~~

{% code title="event message sample" %}
```json
  // 그리기공유종료 알림
  {
      eventOp: 'presence',
      type: 'drawingShareStop',
      user: 'kpoint123',
      roomId: 'K43254033'
  }
```
{% endcode %}

#### ~~type: 'drawingShareImg'~~

{% code title="event message sample" %}
```json
  // 그리기종료 후 이미지 전송
  {
      eventOp: 'presence',
      type: 'drawingShareImg',
      user: 'kpoint123',
      roomId: 'K43254033',
      img: 'img data...'
  }
```
{% endcode %}

#### ~~type: 'drawingClassStop'~~

{% code title="event message sample" %}
```json
  // 미술수업종료 알림
  {
      eventOp: 'presence',
      type: 'drawingClassStop',
      user: 'kpoint123',
      roomId: 'K43254033'
  }
```
{% endcode %}
