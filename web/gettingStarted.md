# Getting Started

## SDK 설치 (Static Import)

{% code title="index.html" %}
```html
<!-- SDK 설치 -->
<script type="text/javascript" src="https://dev.knowledgetalk.co.kr:7102/knowledgetalk.min.js"></script>

<!-- index.js 연결 -->
<script type="test/javascript" src="index.js"></script>
```
{% endcode %}

## SDK 객체 생성

{% code title="index.js" %}
```javascript
// SDK 객체 생성()
let knowledgetalk = new Knowledgetalk();
```
{% endcode %}

## 서버 연결

{% code title="index.js" %}
```javascript
// 서버 연결(userId, name, dvice)
knowledgetalk.init('kpoint123', '홍길동', 'Galaxy Tab');
```
{% endcode %}

* **요청**

| **파라미터** | **타입** | **필수 여부** |   **설명**   |   **예시**   |
| :------: | :----: | :-------: | :--------: | :--------: |
|  userId  | String |     N     | 요청할 userId |  kpoint123 |
|   name   | String |     N     |   사용할 닉네임  |     홍길동    |
|  device  | String |     N     |    기기 정보   | Galaxy Tab |

*   **응답**

    성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))

| **파라미터** | **타입** | **필수 여부** |      **설명**      |   **예시**  |
| :------: | :----: | :-------: | :--------------: | :-------: |
|  userId  | String |     Y     | 랜덤 또는 요청된 userId | kpoint123 |

## 서버 종료

{% code title="index.js" %}
```javascript
// 서버 종료()
knowledgetalk.disconnect();

// SDK 객체 삭제
knowledgetalk = null;
```
{% endcode %}
