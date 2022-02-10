# 이벤트 메시지

  다른 참여자들의 입장, 퇴장 등 상태 등 클라이언트에서 서버로 부터 오는 이벤트 메시지들에 대한 설명
 
## 이벤트 메시지 알림
{% code title="index.js" %}
```javascript
// 이벤트 메시지 알림
knowledgetalk.addEventListener('presence', async event => {
    // 이벤트 메시지 
    let msg = event.detail;

    // 타입별 분기
    switch(msg.type){
    case 'join':
        break;
    }
}
```
{% endcode %}
  
# 타입별 상세 메시지 예시
 
### type: 'join'
{% code title="event message sample" %}
```json
  // 다른 사용자의 입장 알림
  {
      eventOp: 'presence',
      type: 'join',
      roomId: 'K43254033',
      user: { userId: 'kpoint123', name: '홍길동', video: true, audio: true }
  }
```
{% endcode %}
 
### type: 'leave'
{% code title="event message sample" %}
```json
  // 다른 사용자의 퇴장 알림 
  {
      eventOp: 'presence',
      type: 'leave',
      roomId: 'K43254033',
      user: 'kpoint123'
  }
```
{% endcode %}
 
### type: 'publish'
{% code title="event message sample" %}
```json
  // 미디어 서버에서 수신 가능한 사용자들의 영상 알림
  {
      eventOp: 'presence',
      type: 'publish',
      roomId: 'K43254033',
      feeds: [ { id: 'kpoint123', type: 'cam', video: true, audio: true }, { id: 'knowledge123', type: 'cam', video: true, audio: false } ]
  }
```
{% endcode %}
 
### type: 'subscribed'
{% code title="event message sample" %}
```json
  // 해당 사용자의 영상에 대한 P2P 연결 완료 알림
  {
      eventOp: 'presence',
      type: 'subscribed',
      user: 'kpoint123',
      type: 'cam'
  }
```
{% endcode %}
 
### type: 'screen'
{% code title="event message sample" %}
```json
  // 화면공유 알림
  {
      eventOp: 'presence',
      type: 'screen',
      roomId: 'K43254033',
      user: 'kpoint123'
  }
```
{% endcode %}

### type: 'whiteBoard'
{% code title="event message sample" %}
```json
  // 화이트보드 알림
  {
      eventOp: 'presence',
      type: 'whiteboard',
      roomId: 'K43254033',
      user: 'kpoint123'
  }
```
{% endcode %}

### type: 'document'
{% code title="event message sample" %}
```json
  // 자료공유 알림
  {
      eventOp: 'presence',
      type: 'document',
      roomId: 'K43254033',
      user: 'kpoint123'
  }
```
{% endcode %}

### type: 'documentShare'
{% code title="event message sample" %}
```json
  // 이미지 링크 알림
  {
      eventOp: 'presence',
      type: 'documentShare',
      roomId: 'K43254033',
      user: 'kpoint123',
      img: 'img url...'
  }
```
{% endcode %}
 
### type: 'shareStop'
{% code title="event message sample" %}
```json
  // 공유 중지 알림
  {
      eventOp: 'presence',
      type: 'shareStop',
      roomId: 'K43254033',
      user: 'kpoint123'
  }
```
{% endcode %}
 
### type: 'chat'
{% code title="event message sample" %}
```json
  // 채팅 메시지 알림
  {
      eventOp: 'presence',
      type: 'chat',
      user: 'kpoint123',
      message: 'Hello!'
  }
```
{% endcode %}
 
### type: 'inform'
{% code title="event message sample" %}
```json
  // 메시지 수신 알림
  {
      eventOp: 'presence',
      type: 'inform',
      user: 'kpoint123',
      message: 'Hello123'
  }
```
{% endcode %}
 
### type: 'editUserInfo'
{% code title="event message sample" %}
```json
  // 사용자 정보 변경 알림
  {
      eventOp: 'presence',
      type: 'editUserInfo',
      user: 'kpoint123',
      name: 'tom',
      video: true,
      audio: false
  }
```
{% endcode %}
 
### type: 'deviceChanged'
{% code title="event message sample" %}
```json
  // 시스템 오디오 입력 디바이스 변경 알림
  {
      eventOp: 'presence',
      type: 'deviceChanged'
  }
```
{% endcode %}
 
### type: 'createGroup'
{% code title="event message sample" %}
```json
  // 분반 생성 알림
  {
      eventOp: 'presence',
      type: 'createGroup',
      user: 'kpoint123',
      groupId: 'knowledgegroup'
  }
```
{% endcode %}