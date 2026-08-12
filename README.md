# Knowledgetalk

## 환영합니다.

이 문서는 Knowledgetalk SDK 사용법을 설명합니다.\
SDK를 사용하려면 라이센스를 발급받아야 하며 날리지포인트의 허가 없이 수정 및 재배포를 금합니다.

Knowledgetalk는 웹 브라우저에서 P2P·그룹 영상 통화와 채팅, 화면 공유, 분반, 사생활 보호 등 실시간 커뮤니케이션 기능을 구현할 수 있는 SDK입니다.

> **시각화(placeholder)**  
> TODO: SDK 기능 구성도

### 기능 맵

| 기능 | 문서 |
| ---- | ---- |
| 시작하기 (설치·서버 연결) | [Getting Started](web/gettingStarted.md) |
| 방 생성·입장·권한 | [방 관련 기능](web/room.md) |
| 영상 송수신 | [영상 연결 기능](web/media.md) |
| 채팅 | [채팅 기능](web/chatting.md) |
| 화면 공유·캔버스·자료 공유 | [공유 기능](web/share.md) |
| 분반 | [분반 기능](web/group.md) |
| 사생활 보호 | [사생활 보호 기능](web/privacy.md) |
| 이벤트 (presence) | [이벤트 메시지](web/event.md) |

### 권장 구현 순서

1. [Getting Started](web/gettingStarted.md)로 SDK 설치 및 `init` 완료
2. [P2P 샘플](sample/p2p.md) 또는 [그룹 샘플](sample/group.md)로 통화 연결 흐름 확인
3. 필요한 부가 기능 문서의 **호출 전 / 유의사항 / 호출 후**를 따라 구현  
   (API 시그니처만 보고 호출하면 스트림·DOM·presence 처리가 빠지기 쉽습니다)

### 개발절차

#### 라이센스 키 발급

{% embed url="http://knowledgepoint.co.kr/developer/test/list" %}
라이센스 신청
{% endembed %}
