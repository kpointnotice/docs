# 분반 기능

<br>

## 분반 시작

{% code title="index.js" %}
```javascript
// 분반 생성(list, title)
await knowledgetalk.createGroup(list, title);
```
{% endcode %}

- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              list             |           Array           |                N               |     분반에 참여할 사용자들     | ['kpoint123', 'knowledge123'] | 
|             title             |          String           |                N               |            방 제목            |           chatRoom            | 

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. [(=> 응답 코드 바로가기)](https://docs.knowledgetalk.co.kr/web/code)

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             groupId           |           String          |                Y               |          분반 아이디          |          knowledgeGroup       |

<br>

## 분반 종료

{% code title="index.js" %}
```javascript
// 분반 종료(groupId)
await knowledgetalk.endGroup(groupId);
```
{% endcode %}

- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|            groupId            |           String          |                N               |           분반 아이디         |         knowledgeGroup         |

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. [(=> 응답 코드 바로가기)](https://docs.knowledgetalk.co.kr/web/code)