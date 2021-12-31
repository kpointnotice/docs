# 공유 기능

## 화면 공유 시작

{% code title="index.js" %}
```javascript
// 화면 공유 시작(stream, userId, canvas)
await knowledgetalk.screenStart(stream, 'kpoint123', canvas);
```
{% endcode %}

- **요청**
  
  <mark style="color:red;">**canvasInit() / drawingInit()가 포함되어 있으므로 따로 요청하지 않아도 됨**</mark>

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              stream           |       video stream        |                Y               |           영상 스트림         |                               |         
|              target           |          String           |                N               | 일대일인 경우, 상대방의 userId |          kpoint123            |   
|              canvas           |      HTML canvas tag      |                N               |    공유 화면 위의 캔버스 기능  |                               | 

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.

## 캔버스 기능 시작

{% code title="index.js" %}
```javascript
// 캔버스 기능 시작(canvas)
await knowledgetalk.whiteBoardStart(canvas);
```
{% endcode %}

- **요청**

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             canvas            |      HTML canvas tag      |                Y               |           캔버스 태그         |                                | 

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.

  <mark style="color:red;">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨**</mark>

## 캔버스 초기 설정

{% code title="index.js" %}
```javascript
// 캔버스 초기 설정(canvas)
knowledgetalk.canvasInit(canvas);
```
{% endcode %}

- **요청**

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             canvas            |      HTML canvas tag      |                Y               |          캔버스 태그           |                              | 
 
## 캔버스 그리기 시작

{% code title="index.js" %}
```javascript
// 캔버스 그리기 시작 (mousedown, mouseup, mousemove, mouseout, touchstart, touchend, touchcancel, touchmove)
knowledgetalk.drawingInit();
```
{% endcode %}
 
## 캔버스 그리기 종료

{% code title="index.js" %}
```javascript
// 캔버스 그리기 종료 (mousedown, mouseup, mousemove, mouseout, touchstart, touchend, touchcancel, touchmove)
knowledgetalk.drawingStop();
```
{% endcode %}

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.
 
## 그리기 도구 설정

{% code title="index.js" %}
```javascript
// 그리기 도구 설정 (tool, color, stroke width)
knowledgetalk.setTool('pen', 'black', 1);
```
{% endcode %}

- **요청**

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              tool             |           String          |                Y               |     그리기 도구(pen, eraser)   |             pen               |
|             color             |           String          |                N               |        색깔(pen, eraser)       |            black              |
|          stroke width         |           number          |                Y               |         그리기 도구 굵기        |              1                | 
 
## 그림 지우기

{% code title="index.js" %}
```javascript
// 그림 지우기();
knowledgetalk.canvasClear();
```
{% endcode %}
 
## 공유 기능 시작

{% code title="index.js" %}
```javascript
// 공유 기능 시작(canvas)
await knowledgetalk.documentStart(canvas);
```
{% endcode %}

- **요청**

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             canvas            |      HTML canvas tag      |                Y               |           캔버스 태그          |                              | 

- **응답**

  성공 혹은 실패 시에는 Boolean 타입인 true / false를 리턴합니다.
  
  <mark style="color:red;">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨**</mark>

## 자료 공유

{% code title="index.js" %}
```javascript
// 자료 공유(url)
await knowledgetalk.documentShare('https://imgURL');
```
{% endcode %}

- **요청**

| <center>**Pararmeter**</center> | <center>**Type**</center> | <center>**Required**</center> |   <center>**Description**</center>   |   <center>**Example**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              url              |           String          |                Y               |        공유할 이미지 URL       |         https://imgURL       | 

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))
 
## 공유 기능 종료

{% code title="index.js" %}
```javascript
// 공유 기능 종료()
await knowledgetalk.shareStop();
```
{% endcode %}

- **응답**

  성공 혹은 실패 시에는 응답 코드로 리턴합니다. ([응답 코드 바로가기](code.md))