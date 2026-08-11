# 영상 연결 기능

## 미디어 서버에 영상 송신

* **예시**

{% code title="index.js" %}
```javascript
const stream = await navigator.mediaDevices.getUserMedia({ video: true });

await knowledgetalk.publishVideo('cam', stream);
```
{% endcode %}



* **타입**

```typescript
publishvideo(
    type: 'cam';
    stream: MediaStream;
): Promise<boolean>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>type</td><td>'cam'</td><td>'cam'</td></tr><tr><td>stream</td><td>서버와 연결할 영상 스트림</td><td>MediaStream</td></tr></tbody></table>



* **응답 상세**\
  성공 시 true, 실패 시 false



* **호출시 publish 이벤트 메시지 보냄**\
  [이벤트 처리 예시 보기](event.md#type-publish)



## 미디어 서버에 영상 수신

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.subscribeVideo('kpoint123', 'cam');
```
{% endcode %}



* **타입**

```typescript
subscribeVideo(
    userId: string;
    type: 'cam' | 'screen';
): Promise<MediaStream | false>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>userId</td><td>상대방의 유저 아이디</td><td>'kpoint123'</td></tr><tr><td>type</td><td><ul><li>cam: <a href="media.md#undefined">publishVideo</a>로 배포된 영상 수신</li><li>screen: <a href="share.md#undefined">screenStart</a>로 배포된 영상 수신</li></ul></td><td>'cam'</td></tr></tbody></table>



* **응답 상세**

성공 시 상대방 video stream 리턴, 실패 시 false 리턴





## P2P 영상 전송

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.publishP2P("kpoint123", "cam", stream);
```
{% endcode %}



* **타입**

```typescript
publishP2P(
    userId: string;
    type: 'cam';
    stream: MediaStream;
): Promise<boolean>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>userId</td><td>영상을 받을 상대방 유저 아이디</td><td>'kpoint123'</td></tr><tr><td>type</td><td>'cam'</td><td>'cam'</td></tr><tr><td>stream</td><td>영상 스트림</td><td>MediaStream</td></tr></tbody></table>



*   **응답 상세**

    성공 시 true, 실패 시 false 리턴



* **호출시 상대방에게 subscribed 이벤트 메시지  보냄**\
  [이벤트 처리 예시 보기](event.md#type-subscribed)





## 피어 종료

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.removePeer("kpoint123", "cam");
```
{% endcode %}



* **타입**

```typescript
removePeer(
    target: string;
    type: 'cam' | 'screen';
): Promise<boolean>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>target</td><td>종료할 피어의 아이디</td><td>'kpoint123'</td></tr><tr><td>type</td><td>cam / screen 구분</td><td>'cam'</td></tr></tbody></table>



*   **응답 상세**

    성공 시 true, 실패 시 false 리턴





## 영상 정보 변경

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.changeLocalStream(stream, target);
```
{% endcode %}



* **타입**

```typescript
changeLocalStream(
    stream: MediaStream;
    target?: string;
)
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>stream</td><td>새로 변경될 영상 스트림</td><td>MediaStream</td></tr><tr><td>target</td><td>p2p인 경우 상대방 USER ID</td><td>'kpoint123'</td></tr></tbody></table>



*   **응답 상세**

    성공 시 true, 실패 시 false

---

## 영상 송수신 시나리오와 presence

카메라 영상도 API 호출과 presence가 한 세트입니다. **그룹**은 `publish` → `subscribeVideo`, **P2P**는 `subscribed` → `getStream` 패턴이 다릅니다.

> **시각화(placeholder)**  
> TODO: publishVideo / publishP2P ↔ presence publish·subscribed 시퀀스

### 호출 전

* 방 입장 완료, `presence` 리스너 등록
* `getUserMedia`로 로컬 스트림 획득 및 (선택) 로컬 preview video 연결
* 상대 video DOM을 만들 헬퍼 준비

### 유의사항

* 그룹: `publishVideo('cam', stream)` 후 상대는 `publish` 이벤트의 `feed.type === 'cam'`으로 수신합니다.
* P2P: `publishP2P(userId, 'cam', stream)` 후 상대는 `subscribed` (`cam: true`)에서 `getStream(user)`로 받습니다.
* 화면 공유(`screen`) 분기는 [공유 기능](share.md) 문서를 참고하세요.

### 상대 이벤트 수신 시 (presence)

| type | 언제 | 앱에서 할 일 예시 |
| ---- | ---- | ----------------- |
| `publish` (`feed.type === 'cam'`) | 그룹에서 상대가 카메라 publish | `subscribeVideo(id, 'cam')` → video `srcObject` |
| `subscribed` (`cam: true`) | P2P에서 상대 카메라 연결 완료 | `getStream(user)` → video `srcObject` |

{% code title="presence - cam publish (group)" %}
```javascript
knowledgetalk.addEventListener('presence', async (event) => {
  const msg = event.detail;

  switch (msg.type) {
    case 'publish': {
      for (const feed of msg.feeds) {
        const stream = await knowledgetalk.subscribeVideo(feed.id, feed.type);

        if (feed.type === 'cam') {
          createVideoBox(feed.id);
          document.getElementById('multiVideo-' + feed.id).srcObject = stream;
        }
      }
      break;
    }

    case 'subscribed': {
      // P2P
      const { cam, user } = msg;
      if (cam) {
        createVideoBox(user);
        document.getElementById('multiVideo-' + user).srcObject =
          knowledgetalk.getStream(user);
      }
      break;
    }
  }
});
```
{% endcode %}

* 타입 상세: [publish](event.md#type-publish), [subscribed](event.md#type-subscribed)
* 샘플: [그룹 샘플](../sample/group.md), [P2P 샘플](../sample/p2p.md)

