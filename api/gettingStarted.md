# Getting Started

## 개요
- 본 문서는 Web Browser와 Signal Server 사이의 개발 연동을 위한 제반 사항을 기술한다.
## API 사용 유의사항
1. 인증 정보(CP Code, Auth Key)를 발급하여 접속하는 클라이언트에게 제공한다.
2. 인증 정보를 제공받은 클라이언트는 API(register) 요청 시 인증 정보를 포함시킨다.
3. Server 에서는 해당 인증 정보를 가지고 API 허용 여부를 결정하여 처리한다.

    [sample]

        {
            cpCode: 'CPOFSECRET’,
            authKey: 'XJCJ535JKF23KRJL....'
        }

4. TURN 서버 연동 가이드 및 연동 시 유의사항 (아래 정책을 따르지 않으면 네트워크 사용량에 따라 기본 요금제 외의 별도 비용이 발생 할 수 있음)
   - 원활한 영상 통신을 위해 KnowledgeTalk 에서는 STUN/TURN 서버를 운영 중임(register 요청 시, 응답으로 리턴)
   - 각 개발사의 자체 STUN/TURN 이용하거나 기존 Open 된 free STUN/TURN (구글 STUN 서버 등)을 이용해도 무방함. KnowledgeTalk STUN/TURN 사용하는 경우 아래와 같이 적용.
   - RTCPeerConnection 생성 시 iceServers configuration에 STUN/TURN 서버 정보를 추가 할 수 있음. 

## 연동 방법(라이센스 발급 시, 상용 정보는 별도 제공)
[개발용 연동 정보]
- Server URL : https://dev.knowledgetalk.co.kr:7102
  - 상기 URL로 Socket 연결이 필요합니다.
  - https://dev.knowledgetalk.co.kr:7102/socket.io/socket.io.min.js import 해서 사용해야함.
  - 모든 규격은 JSON(Object) 형태로 전송해야 합니다.
