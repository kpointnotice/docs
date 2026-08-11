# 영상 연결 기능

## 카메라 권한에 따른 입장 정책

KnowledgeTalk SDK의 `joinRoom()`은 카메라 권한을 확인하지 않습니다. 카메라 권한이 없어도 방에 입장할 수 있으므로, 서비스 요구사항에 따라 클라이언트에서 입장 정책을 결정해야 합니다.

### 카메라 권한이 필수인 경우

카메라 권한을 먼저 요청하고 스트림 생성에 성공한 경우에만 `joinRoom()`을 호출합니다. 사용자가 권한을 거부하면 안내 메시지를 표시하고 입장 절차를 중단합니다.

{% code title="index.js" %}
```javascript
const joinWithRequiredCamera = async () => {
    let localStream;

    try {
        localStream = await navigator.mediaDevices.getUserMedia({ video: true });
    } catch (error) {
        if (error.name === 'NotAllowedError') {
            // 서비스 UI에서 카메라 권한을 안내한 후 입장 중단
            return;
        }

        throw error;
    }

    const roomData = await knowledgetalk.joinRoom('K43254033');

    if (roomData.code === '200') {
        await knowledgetalk.publishVideo('cam', localStream);
    }
};

await joinWithRequiredCamera();
```
{% endcode %}

### 카메라 없이 입장을 허용하는 경우

카메라 권한 거부를 카메라 미사용 상태로 처리하고 `joinRoom()`을 계속 호출합니다. 카메라 스트림이 없으므로 `publishVideo()`는 호출하지 않지만, 상대방 영상은 기존 수신 절차에 따라 볼 수 있습니다.

{% code title="index.js" %}
```javascript
const joinWithOptionalCamera = async () => {
    let localStream = null;

    try {
        localStream = await navigator.mediaDevices.getUserMedia({ video: true });
    } catch (error) {
        if (error.name !== 'NotAllowedError') throw error;

        // 카메라 없이 수신 전용으로 입장
        localStream = null;
    }

    const roomData = await knowledgetalk.joinRoom('K43254033');

    if (roomData.code !== '200') return;

    if (localStream) {
        await knowledgetalk.publishVideo('cam', localStream);
    }
};

await joinWithOptionalCamera();
```
{% endcode %}

카메라 없이 입장한 사용자는 자신의 카메라 영상을 송신하지 않습니다. 상대방 영상은 기존 [`publish` 이벤트](event.md#type-publish)와 `subscribeVideo()` 절차를 통해 수신할 수 있습니다.



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



