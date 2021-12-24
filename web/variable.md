# 전역 변수

Knowledgepoint() 객체 내부에서 사용되는 전역 변수에 대한 소개입니다.

    {% code title="index.js" %}
    ```javascript
    // SDK 객체 생성
    let knowledgeTalk = new KnowledgeTalk();
    ```
    {% endcode %}

아래의 함수들은 위에서 생성된 SDK객체를 예로 각각의 변수를 호출명으로 가져오는 예제입니다.

## userId 조회
{% code title="index.js" %}
```javascript
// userId 조회
let userId = knowledgetalk.getUserId();
```
{% endcode %}

## roomId 조회
{% code title="index.js" %}
```javascript
// roomId 조회
let roomId = knowledgetalk.getRoomId();
```
{% endcode %}

## socket 객체
{% code title="index.js" %}
```javascript
// socket 객체
let socket = knowledgetalk.getSocket();
```
{% endcode %}

## 모든 peer 정보
{% code title="index.js" %}
```javascript
// 모든 peer 정보
let allPeers = knowledgetalk.getAllPeers();
```
{% endcode %}

## id로 peer 조회
{% code title="index.js" %}
```javascript
// id로 peer 조회
let userPeer = knowledgetalk.getPeers(id);
```
{% endcode %}

## 모든 stream 정보
{% code title="index.js" %}
```javascript
// 모든 stream 정보
let allStreams = knowledgetalk.getAllStreams();
```
{% endcode %}

## id로 stream 조회
{% code title="index.js" %}
```javascript
// id로 stream 조회(id)
let userStream = knowledgetalk.getStream(id);
```
{% endcode %}

## 미디어서버 사용 여부
{% code title="index.js" %}
```javascript
// 미디어서버 사용 여부
let media = knowledgetalk.isMedia();
```
{% endcode %}

## 공유 타입
{% code title="index.js" %}
```javascript
// 공유 타입
let shareType = knowledgetalk.getShareType()
```
{% endcode %}

## 닉네임 조회
{% code title="index.js" %}
```javascript
// 사용자의 userId 조회
let name = knowledgetalk.getName();
```
{% endcode %}