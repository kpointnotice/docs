# 공유 기능

## 화면 공유 시작

* **예시**

{% code title="index.js" %}
```javascript
const stream = await navigator.mediaDevices.getDisplayMedia({ video: true });

await knowledgetalk.screenStart(stream, 'kpoint123', canvas);
```
{% endcode %}



* **타입**

```typescript
screenStart(
    stream: MediaStream;
    target?: string;
    canvas?: HTMLCanvasElement;
): Promise<boolean>;
```



*   **요청 상세**

    <mark style="color:red;">**canvasInit() / drawingInit()가 포함되어 있으므로 따로 요청하지 않아도 됨**</mark>

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>stream</td><td>공유할영상 스트림</td><td>MediaStream</td></tr><tr><td>target</td><td>P2P 경우, 상대방의 userId</td><td>'kpoint123'</td></tr><tr><td>canvas</td><td>공유 화면 위의 캔버스 기능</td><td>HTMLcanvasElement</td></tr></tbody></table>



*   **응답 상세**

    성공 시  true 실패 시false를 리턴합니다.
* 타겟 유저는 [screen 이벤트 메시지](event.md#type-screen) 받아 사용





## 캔버스 기능 시작

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.whiteBoardStart(canvas);
```
{% endcode %}



* **타입**

```typescript
whiteBoardStart(
    canvas: HTMLcanvasElement;
): Promise<boolean>;
```



* **요청 상세**\
  <mark style="color:red;">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨**</mark>

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>canvas</td><td>캔버스 태그</td><td>HTMLcanvasElement</td></tr></tbody></table>



*   **응답 상세**

    성공 시  true 실패 시false를 리턴합니다.
* 타겟 유저는 [whiteBoard 이벤트 메시지](event.md#type-whiteboard)를 받아 사용





## 캔버스 초기 설정

* **예시**

{% code title="index.js" %}
```javascript
knowledgetalk.canvasInit(canvas);
```
{% endcode %}



* **타입**

```typescript
canvasInit(
    canvas: HTMLCanvasElement;
): void;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>canvas</td><td>캔버스 태그</td><td>HTMLcanvasElement</td></tr></tbody></table>





## 캔버스 그리기 시작

_mousedown, mouseup, mousemove, mouseout, touchstart, touchend, touchcancel, touchmove_ \
_이벤트를 추가합니다._\


* **예시**

{% code title="index.js" %}
```javascript
knowledgetalk.drawingInit();
```
{% endcode %}



* **타입**

```typescript
drawingInit():boolean;
```



* **응답 상세**\
  성공 시  true 실패 시false를 리턴합니다.





## 캔버스 그리기 종료

_mousedown, mouseup, mousemove, mouseout, touchstart, touchend, touchcancel, touchmove_ \
_이벤트를 제거합니다._\


* **예시**

{% code title="index.js" %}
```javascript
knowledgetalk.drawingStop();
```
{% endcode %}



* **타입**

```typescript
drawingStop(): boolean;
```



* **응답 상세**\
  성공 시  true 실패 시false를 리턴합니다.





## 캔버스 동기화 요청

_<mark style="color:red;">**입장 시, 판서 중인 경우 판서 중인 상대에게 판서 정보 요청해서 동기화 진행(canvasInit 완료 후 요청)**</mark>_

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.reqCanvasImage(target);
```
{% endcode %}



* **타입**

```typescript
reqCanvasImage(
    target: string;
): Promise<{
    code: ResponseCode
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>target</td><td>해당 userId에게 메시지 전송</td><td>'kpoint123'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>





## 그리기 도구 설정

* **예시**

{% code title="index.js" %}
```javascript
knowledgetalk.setTool('pen', 'black', 1);
```
{% endcode %}



* **타입**

```typescript
setTool(
    tool: 'pen' | 'eraser' | 'shape' | 'pointer' | 'textbox';
    color?: string;
    strokeWidth: number;
    type?: ShapeType | 'highlight';
): void;
```

```typescript
type ShapeType = "arrow" | "circle" | "hand" | "heart" | "line" | "square" | "star" | "triangle" | "important" | "check";          
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>tool</td><td>그리기 도구</td><td>'pen'</td></tr><tr><td>color</td><td>색깔</td><td>'black'</td></tr><tr><td>strokeWidth</td><td>그리기 도구 굵기</td><td>1</td></tr><tr><td>type</td><td><ul><li>형광펜: tool이 pen일 경우 highlight</li><li>도형: tool이 shape일 경우 ShapeType</li><li>그 외 생략</li></ul></td><td></td></tr></tbody></table>





## 그림 지우기

* **예시**

{% code title="index.js" %}
```javascript
knowledgetalk.canvasClear();
```
{% endcode %}





## 공유 기능 시작

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.documentStart(canvas);
```
{% endcode %}



* **타입**

```typescript
documentStart(
   canvas: HTMLCanvasElement;
): Promise<{
   code: ResponseCode;
}> 
```



* **요청 상세**\
  <mark style="color:red;">**canvasInit() / drawingInit() 가 포함되어 있으므로 따로 요청하지 않아도 됨**</mark>

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>canvas</td><td>공유화면 위의 캔버스 기능</td><td>HTMLcanvasElement</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* [document 이벤트 메시지](event.md#type-document) 받아 사용





## 자료 공유

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.documentShare('https://imgURL');
```
{% endcode %}



* **타입**

```typescript
documentShare(
    imgUrl: string;
): Promise<{
    code: ResponseCode;
}>
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>imgUrl</td><td>공유할 이미지 URL</td><td>'https://imgURL'</td></tr></tbody></table>



* **응답**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* [documentShare 이벤트 메시지](event.md#type-documentshare) 받아 사용





## 공유 기능 종료

* **예시**

{% code title="index.js" %}
```javascript
await knowledgetalk.shareStop();
```
{% endcode %}



* **타입**

```typescript
shareStop(): Promise<{
    code: ResponseCode;
}>
```



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>code</td><td><a href="code.md">응답 코드 바로가기</a></td><td>'200'</td></tr></tbody></table>

* [shareStop 이벤트 메시지](event.md#type-sharestop) 받아 사용



