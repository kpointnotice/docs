# 분반 기능
 
## 분반 시작

{% code title="index.js" %}
```javascript
// 분반 생성(list, title)
await knowledgetalk.createGroup(list, title);
```
{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              list             |           Array           |                N               |     분반에 참여할 사용자들     | ['kpoint123', 'knowledge123'] | 
|             title             |          String           |                N               |            방 제목            |           chatRoom            | 

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             groupId           |           String          |                Y               |          분반 아이디          |          knowledgeGroup       |
 
## 분반 종료

{% code title="index.js" %}
```javascript
// 분반 종료(groupId)
await knowledgetalk.endGroup(groupId);
```
{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|            groupId            |           String          |                N               |           분반 아이디         |         knowledgeGroup         |

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))