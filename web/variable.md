# 전역 변수

 Knowledgepoint() 객체 내부에 사용되는 전역 변수들의 모음입니다.

## userId 조회
{% code title="index.js" %}
```javascript
// userId 조회
getUserId = () => this.#userid;
```
{% endcode %}

## roomId 조회
{% code title="index.js" %}
```javascript
// roomId 조회
getRoomId = () => this.#roomid;
```
{% endcode %}

## socket 객체
{% code title="index.js" %}
```javascript
// socket 객체
getSocket = () => this.#socket;
```
{% endcode %}

## 모든 peer 정보
{% code title="index.js" %}
```javascript
// 모든 peer 정보
getAllPeers = () => this.#peers;
```
{% endcode %}

## id로 peer 조회
{% code title="index.js" %}
```javascript
// id로 peer 조회(id)
getPeers = id => this.#peers[id];
```
{% endcode %}

## 모든 stream 정보
{% code title="index.js" %}
```javascript
// 모든 stream 정보
getAllStreams = () => this.#streams;
```
{% endcode %}

## id로 stream 조회
{% code title="index.js" %}
```javascript
// id로 stream 조회(id)
getStream = id => this.#streams[id];
```
{% endcode %}

## 미디어서버 사용 여부
{% code title="index.js" %}
```javascript
// 미디어서버 사용 여부
isMedia = () => this.#media;
```
{% endcode %}

## 공유 타입
{% code title="index.js" %}
```javascript
// 공유 타입
getShareType = () => this.#shareType;
```
{% endcode %}

## 닉네임 조회
{% code title="index.js" %}
```javascript
// 사용자의 userId 조회
getName = () => this.#name;
```
{% endcode %}

