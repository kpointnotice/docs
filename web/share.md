# 공유 기능

## 회면 공유 기능 시작

{% code title="index.js" %}
```javascript
//화면 공유 시작 요청
await knowledgetalk.screenStart(stream, 'kpoint', canvas);
```
{% endcode %}

- **요청**

| 파라미터 |      타입       | 필수 여부 |  예시  |               설명               |
| :------: | :-------------: | :-------: | :----: | :------------------------------: |
|  stream  |  video stream   |     Y     |        |           영상 스트림            |
|  target  |     string      |     N     | kpoint |     일대일인 경우, 상대방 ID     |
|  canvas  | HTML canvas tag |     N     |        | 공유 화면 위에 판서 기능 사용 시 |

- **응답**

  성공 시 true, 실패 시 false 리턴

- <span style="color:red">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨.**</span>

## 화이트 보드 기능 시작

{% code title="index.js" %}
```javascript
//화이트 보드 시작 요청
await knowledgetalk.whiteBoardStart(canvas);
```
{% endcode %}

- **요청**

| 파라미터 |      타입       | 필수 여부 | 예시 |    설명     |
| :------: | :-------------: | :-------: | :--: | :---------: |
|  canvas  | HTML canvas tag |     Y     |      | 캔버스 태그 |

- **응답**

  성공 시 true, 실패 시 false 리턴

- <span style="color:red">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨.**</span>


## 캔버스 초기 설정

{% code title="index.js" %}
```javascript
//캔버스 설정 
knowledgetalk.canvasInit(canvas);
```
{% endcode %}

- **요청**

| 파라미터 |      타입       | 필수 여부 | 예시 |    설명     |
| :------: | :-------------: | :-------: | :--: | :---------: |
|  canvas  | HTML canvas tag |     Y     |      | 캔버스 태그 |

## 그리기 시작

{% code title="index.js" %}
```javascript
//캔버스에 그리기 이벤트 추가 (mousedown, mouseup, mousemove, mouseout, touchstart, touchend, touchcancel, touchmove)
knowledgetalk.drawingInit();
```
{% endcode %}


## 그리기 종료

{% code title="index.js" %}
```javascript
//이벤트 제거 (mousedown, mouseup, mousemove, mouseout, touchstart, touchend, touchcancel, touchmove)
knowledgetalk.drawingStop();
```
{% endcode %}

- **응답**

  성공 시 true, 실패 시 false 리턴

## 그리기 도구 설정

{% code title="index.js" %}
```javascript
//그리기 도구 설정
knowledgetalk.setTool('pen', 'black', 1);
```
{% endcode %}

- **요청**

|   파라미터   |  타입  | 필수 여부 | 예시  |           설명           |
| :----------: | :----: | :-------: | :---: | :----------------------: |
|     tool     | string |     Y     |  pen  | 그리기 도구(pen, eraser) |
|    color     | string |     N     | black |    색깔(pen, eraser)     |
| stroke width | string |     Y     |   1   |        도구 굵기         |

## 자료 공유 시작

{% code title="index.js" %}
```javascript
//자료공유 시작 요청
await knowledgetalk.documentStart(canvas);
```
{% endcode %}

- **요청**

| 파라미터 |      타입       | 필수 여부 | 예시 |    설명     |
| :------: | :-------------: | :-------: | :--: | :---------: |
|  canvas  | HTML canvas tag |     Y     |      | 캔버스 태그 |

- **응답**

  성공 시 true, 실패 시 false 리턴

- <span style="color:red">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨.**</span>

## 자료 파일 공유

{% code title="index.js" %}
```javascript
//자료공유 시작 요청
await knowledgetalk.documentShare(url);
```
{% endcode %}

- **요청**

| 파라미터 |  타입  | 필수 여부 |      예시       |       설명        |
| :------: | :----: | :-------: | :-------------: | :---------------: |
|   url    | string |     Y     | https://img.url | 공유할 이미지 url |

- **응답**

  응답 코드 리턴

## 공유 기능 종료

{% code title="index.js" %}
```javascript
//공유 중지 요청
await knowledgetalk.shareStop();
```
{% endcode %}

- **응답**

  응답 코드 리턴