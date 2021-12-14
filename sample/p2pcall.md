# P2P 통화 연결하기(WEB)

### 설명

중앙 미디어 서버없이 종단 간 직접 연결하여 발신자는 연결을 하고 싶은 사람에게 내 영상을 보낼 수 있다.
단, NAT/방화벽 환경의 클라이언트가 외부망과의 통신을 위해 공인 IP 정보를 알려줄 수 없는 경우에는 중계 서버를 거쳐서 연결이 된다.

- [샘플 보기](https://dev.knowledgetalk.co.kr:3456/p2p)
- [샘플 소스 코드](https://github.com/kpointnotice/knowledgetalk-sample/blob/master/public/p2p.html)
- [STUN / TURN 설명 보기](https://developer.mozilla.org/ko/docs/Web/API/WebRTC_API/Protocols)

### 개발
1. 서버 연결
{% code title="index.html" %}
```html
//sdk import
<script type="text/javascript" src="https://dev.knowledgetalk.co.kr:7102/knowledgetalk.min.js"></script>
```
{% endcode %}

knowledgetalk sdk 를 사용하기 위해 HTML 파일에서 knowledgetalk sdk file을 import 한다.

{% code title="index.js" %}
```javascript
//객체 생성
let knowledgetalk = new Knowledgetalk();

//서버 연결
knowlegetalk.init('https://dev.knowledgetalk.co.kr:7102').then(result => {
        //연결 실패한 경우
        if(result.code !== '200'){
                
        }

        //성공 시, user id 리턴
        let userId = result.userId;
})
```
{% endcode %}


객체를 생성하고 서버와 연결한다.<br/>
연결이 성공되면 user id를 발급받을 수 있다.

2. 방 생성
{% code title="index.js" %}
```javascript
//성공 시, room id 리턴
await knowledgetalk.createRoom();
```
{% endcode %}

방을 만들고 발급받은 room id를 상대방에게 알려준다.

3. 방 입장
{% code title="index.js" %}
```javascript
//방 입장 요청
await knowledgetalk.joinroom('room1');
```
{% endcode %}

호스트: 만든 방에 입장하여 상대방이 입장할때까지 대기한다.
게스트: 호스트에게 받은 room id로 방에 입장한다.



4. 영상 전송
{% code title="index.js" %}
```javascript
//로컬 영상 불러오기
let localStream = await navigator.mediaDevices.getUserMedia({video: true, audio: false});

//상대방에 stream 전송
await knowledgetalk.publishP2P('kpoint','cam', localStream);
```
{% endcode %}

상대방 user id, cam/screen 구분 type, 로컬 영상을 상대방에게 전송한다.

5. 이벤트 메시지 수신
6. 
{% code title="event message sample" %}
```javascript
//이벤트 메시지 수신
knowledgetalk.addEventListener('presence', async event => {

        let msg = event.detail;
        let type = msg.type;

        switch (type){
                //다른 user 의 입장 알림
                case 'join':
                        createVideoBox(msg.user.userId);             
                        break;
                //다른 user 의 퇴장 알림
                case 'leave':
                        removeVideoBox(msg.user);
                        break;
                //다른 user 의 영상 연결 완료
                case 'subscribed':
                        document.getElementById('multiVideo-' + msg.user).srcObject = knowledgetalk.streams[msg.user];
                        break;
        }       
}
```
{% endcode %}