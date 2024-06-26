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



