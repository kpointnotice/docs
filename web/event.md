# 이벤트 메시지

## 이벤트 메시지 알림
{% code title="index.js" %}
```javascript
//event 메시지 알림
knowledgetalk.addEventListener('presence', async event => {
    //event message 
    let msg = event.detail;

    //타입별 분기
    switch(msg.type){
    case 'join':
        break;
    }
}
```
{% endcode %}
    

## 타입별 상세 메시지 예시

### join
{% code title="event message sample" %}
```json
  // 다른 user의 입장 알림
  {
      eventOp: 'presence',
      type: 'join',
      roomId: 'room1',
      user: { userId: 'kpoint', name: '익명', video: true, audio: true }
  }
```
{% endcode %}

### leave
{% code title="event message sample" %}
```json
  // 다른 user의 퇴장 알림 
  {
      eventOp: 'presence',
      type: 'leave',
      roomId: 'room1',
      user: 'kpoint'
  }
```
{% endcode %}

### publish
{% code title="event message sample" %}
```json
  // 미디어 서버에서 수신 가능한 user들의 영상 알림
  {
      eventOp: 'presence',
      type: 'publish',
      roomId: 'room1',
      feeds: [ { id: 'kpoint', type: 'cam', video: true, audio: true }, { id: 'knowledge', type: 'cam', video: true, audio: false } ]
  }
```
{% endcode %}

### subscribed
{% code title="event message sample" %}
```json
  // 해당 user의 영상에 대한 p2p 연결 완료 알림
  {
      eventOp: 'presence',
      type: 'subscribed',
      user: 'kpoint',
      type: 'cam'
  }
```
{% endcode %}

### screen
{% code title="event message sample" %}
```json
  // 화면공유 알림
  {
      eventOp: 'presence',
      type: 'screen',
      roomId: 'room1',
      user: 'kpoint'
  }
```
{% endcode %}

### shareStop
{% code title="event message sample" %}
```json
  // 공유 중지 알림
  {
      eventOp: 'presence',
      type: 'shareStop',
      roomId: 'room1',
      user: 'kpoint'
  }
```
{% endcode %}

### chat
{% code title="event message sample" %}
```json
  // 공유 중지 알림
  {
      eventOp: 'presence',
      type: 'chat',
      user: 'kpoint',
      message: 'chat msg'
  }
```
{% endcode %}

### inform
{% code title="event message sample" %}
```json
  // 공유 중지 알림
  {
      eventOp: 'presence',
      type: 'inform',
      user: 'kpoint',
      message: 'chat msg'
  }
```
{% endcode %}

### editUserInfo
{% code title="event message sample" %}
```json
  // 유저 정보 변경 알림
  {
      eventOp: 'presence',
      type: 'editUserInfo',
      user: 'kpoint',
      name: 'tom',
      video: true,
      audio: false
  }
```
{% endcode %}

### deviceChanged
{% code title="event message sample" %}
```json
  // 시스템 오디오 입력 디바이스 변경 알림
  {
      eventOp: 'presence',
      type: 'deviceChanged'
  }
```
{% endcode %}

### createGroup
{% code title="event message sample" %}
```json
  // 분반 생성 알림
  {
      eventOp: 'presence',
      type: 'createGroup',
      user: 'kpoint',
      groupId: 'group1'
  }
```
{% endcode %}