# 분반 기능

## 분반 시작

{% code title="index.js" %}
```javascript
//분반 생성
await knowledgetalk.createGroup(list, title);
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 |        예시        |             설명             |
| :------: | :----: | :-------: | :----------------: | :--------------------------: |
|   list   | array  |     N     | ['user1', 'user2'] |     분반에 참여할 리스트     |
|  title   | string |     N     |       방제목       | 원하는 ROOM TITLE 로 방 생성 |

- **응답**

| 파라미터 |  타입  | 필수 여부 |  예시  |    설명     |
| :------: | :----: | :-------: | :----: | :---------: |
|   code   | string |     Y     |  200   |  응답코드   |
| groupId  | string |     Y     | group1 | 분반 아이디 |

## 분반 종료

{% code title="index.js" %}
```javascript
//분반 종료
await knowledgetalk.endGroup(groupId);
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 |  예시  |    설명     |
| :------: | :----: | :-------: | :----: | :---------: |
| groupId  | string |     N     | group1 | 분반 아이디 |

- **응답**

  응답 코드 리턴