# Getting Started

## SDK 설치 - Static Import

{% code title="index.html" %}
```html
//sdk import
<script type="text/javascript" src="knowledgetalk.min.js"></script>
//sdk 사용할 javascript 파일
<script type="test/javascript" sra="index.js"></script>
```
{% endcode %}

## 객체 생성
{% code title="index.js" %}
```javascript
//객체 생성
let knowledgetalk = new Knowledgetalk();
```
{% endcode %}

## 서버 연결
{% code title="index.js" %}
```javascript
//서버 연결 성공 시, user id 리턴
knowlegetalk.init('https://server:port', 'kpoint', '날리지', 'device');
```
{% endcode %}

- **요청**
  
| 파라미터 |  타입  | 필수여부 |        예시        |            설명             |
| :------: | :----: | :------: | :----------------: | :-------------------------: |
|   url    | string |    Y     | https://server.url |      연동할 서버의 URL      |
| user id  | string |    N     |       kpoint       | 원하는 USER ID로 초기 설정  |
|   name   | string |    N     |       날리지       | 원하는 닉네임으로 초기 설정 |
|  device  | string |    N     |     Galaxy Tab     |        디바이스 정보        |

- **응답**

| 파라미터 |  타입  |  예시  |                   설명                   |
| :------: | :----: | :----: | :--------------------------------------: |
| user id  | string | kpoint | 사용자가 요청한 ID 또는 서버가 생성한 ID |

실패 시, error code 리턴