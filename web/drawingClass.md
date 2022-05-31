# 미술 수업 기능

## 미술 수업 시작

{% code title="index.js" %}
```javascript
// 미술 수업 시작
await knowledgetalk.documentClassStart();
```
{% endcode %}

- **요청**

  HOST가 호출

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.

## 그리기 공유 시작

{% code title="index.js" %}
```javascript
// 미술 수업 시작(canvas)
await knowledgetalk.documentShareStart(canvas);
```
{% endcode %}

- **요청**

  GUEST가 호출

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             canvas            |      HTML canvas tag      |                Y               |           캔버스 태그         |                                | 

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.

## 그리기 공유 종료

{% code title="index.js" %}
```javascript
// 그리기 공유 종료
await knowledgetalk.documenShareStop();
```
{% endcode %}

- **요청**

  HOST가 호출

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.

## 미술 수업 종료

{% code title="index.js" %}
```javascript
// 미술 수업 종료
await knowledgetalk.documentClassStop();
```
{% endcode %}

- **요청**

  HOST가 호출

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.