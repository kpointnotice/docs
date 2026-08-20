# Getting Started

## SDK 설치 (Static Import)

{% code title="index.html" %}
```html
<!-- SDK 설치 -->
<script type="text/javascript" src="https://knowledgetalk.co.kr:7104/knowledgetalk.min.js"></script>
```
{% endcode %}



## SDK 객체 생성

```javascript
const knowledgetalk = new Knowledgetalk();
```



## 서버 연결

* **예시**

```javascript
await knowledgetalk.init(
    "KP-20200101-01",
    "eyJhbGciO...",
    "kpoint123",
    "홍길동",
    "Galaxy Tab"
);
```



* **타입**

```typescript
init(
    cpCode: string; 
    authKey: string; 
    id?: string; 
    name?: string;
    device?: string; 
    forced?: boolean; 
): Promise<{
    code: ResponseCode;
    userId: string;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="432">Description</th><th>Example</th></tr></thead><tbody><tr><td>cpCode</td><td>발급 받은 cpCode</td><td>"KP-20200101-01"</td></tr><tr><td>authKey</td><td>발급 받은 authKey</td><td>"eyJhbGciO..."</td></tr><tr><td>id</td><td>요청할 유저 아이디</td><td>"kpoint123"</td></tr><tr><td>name</td><td>사용할 닉네임</td><td>"홍길동"</td></tr><tr><td>device</td><td>기기 정보</td><td>"Galaxy Tab"</td></tr><tr><td>forced</td><td><ul><li>true이면 기존 연결을 끊고 재연결합니다.</li><li>기본값: false</li></ul></td><td>false</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>"200"</td></tr><tr><td>userId</td><td>랜덤 또는 요청된 userId</td><td>"kpoint123"</td></tr></tbody></table>



## 서버 종료

{% code title="index.js" %}
```javascript
// 서버 종료
knowledgetalk.disconnect();

// SDK 객체 삭제
knowledgetalk = null;
```
{% endcode %}

## 다음 단계

서버 연결(`init`)이 끝나면 아래 순서로 이어가면 시행착오를 줄일 수 있습니다.

1. [P2P 샘플](../sample/p2p.md) 또는 [그룹 샘플](../sample/group.md)로 방 입장·영상 송수신 확인
2. 부가 기능은 API 시그니처만이 아니라 **호출 전 / 유의사항 / 호출 후**를 함께 확인  
   * [채팅](chatting.md)  
   * [화면 공유·캔버스](share.md)  
   * [분반](group.md)  
3. 수신·상태 변화는 [이벤트 메시지](event.md)의 `presence` 타입별 처리를 참고합니다.
