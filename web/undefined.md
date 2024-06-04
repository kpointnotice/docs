---
description: 캠 화면에 블러 처리 또는 가상 배경을 적용합니다.
---

# 사생활 보호 기능



## 설치

{% code title="index.html" %}
```html
<script type="text/javascript" src="https://dev.knowledgetalk.co.kr:7102/uncompressed/privacyMode.js"></script>
```
{% endcode %}





## 인스턴스 생성 및 초기화

```typescript
const privacyMode = new PrivacyMode();

await privacyMode.init();
```





## 사생활 보호 시작

* **예시**

```typescript
const blurStream = await privacyMode.start(
      inputVideo,
      outputCanvas,
      'bg',
      'https://imgUrl...',
);
```



* **타입**

```typescript
start(
    inputVideo: HTMLVideoElement;
    outputCanvas: HTMLCanvasElement;
    mode: "blur" | "bg";
    bgSrc: string | null;
): Promise<MediaStream>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>inputVideo</td><td>사생활 보호를 적용할 stream</td><td>HTMLVideoElement</td></tr><tr><td>outputCanvas</td><td>사생활 보호가 적용된 결과물을 보여줄 canvas</td><td>HTMLCanvasElement</td></tr><tr><td>mode</td><td>블러 처리 또는 가상 배경</td><td>'bg'</td></tr><tr><td>bgSrc</td><td>가상 배경 이미지 경로</td><td>'https://imgUrl...'</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>blurStream</td><td>사생활 보호가 적용된 stream</td><td>MediaStream</td></tr></tbody></table>

* blurStream 또는 outputCanvas에 결과물이 표시 됩니다.\
  필요에 따라 stream 또는 canvas 형식으로 사용할 수 있습니다.





## 사생활 보호 영상 송신

기존  스트림을  생활 보호가 적용된 스트림으로 교체합니다.

* **예시**

```typescript
await privacyMode.sendBlurVideoTrack(knowledgetalk);
```



* **타입**

```typescript
sendBlurVideoTrack(
    sdk: Knowledgetalk;
    target?: string;    
): Promise<void>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>sdk</td><td>Knowledgetalk SDK 인스턴스</td><td>Knowledgetalk</td></tr><tr><td>target</td><td>p2p의 경우 타겟 유저 아이디</td><td>'u1234'</td></tr></tbody></table>





## 사생활 보호 배경 변경

[사생활 보호 시작](undefined.md#undefined-2) 후 모드 또는 배경을 변경할 때 호출합니다.

* **예시**

```typescript
await privacyMode.changeBackground('bg', 'https://imageUrl...');
```



* **타입**

```typescript
changeBackground(
    mode: "blur" | "bg";
    bgUrl: string | null;
): Promise<void>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>mode</td><td>변경할 모드</td><td>'bg'</td></tr><tr><td>bgUrl</td><td>bg모드 일 경우 배경 이미지 경로</td><td>'https://imageUrl...'</td></tr></tbody></table>





## 사생활 보호 요소 업데이트

사생활 보호 진행 중 inputVideo 또는 outputCanvas 요소의 변경이 필요한 경우에만 호출합니다.

* **예시**

```typescript
await privacyMode.update(newInputVideoEl, newOutputCanvas);
```



* **타입**

```typescript
update(
    inputVideo: HTMLVideoElement;
    outputCanvas: HTMLCanvasElement;
): Promise<MediaStream>;
```



* **요청 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>inputVideo</td><td>변경할 video element</td><td>HTMLVideoElement</td></tr><tr><td>outputCanvas</td><td>변경할 canvas element</td><td>HTMLCanvasElement</td></tr></tbody></table>



* **응답 상세**

<table><thead><tr><th width="141">Parameter</th><th width="429">Description</th><th>Example</th></tr></thead><tbody><tr><td>blurStream</td><td>사생활 보호가 적용된 새로운 stream</td><td>MediaStream</td></tr></tbody></table>





## 사생활 보호 종료

사생활 보호 스트림을 기존 스트림으로 교체하고 사생활 보호를 종료합니다.&#x20;

* **예시**

```typescript
await privacyMode.stop();
```

















