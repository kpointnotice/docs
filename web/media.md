# 영상 연결 기능

## 미디어 서버에 영상 전송

{% code title="index.js" %}
```javascript
//미디어 서버에 stream 전송 요청
await knowledgetalk.publishVideo('cam', stream);
```
{% endcode %}
    

- **요청**

| 파라미터 |     타입     | 필수 여부 | 예시 |           설명            |
| :------: | :----------: | :-------: | :--: | :-----------------------: |
|   type   |    string    |     Y     | cam  |     cam / screen 구분     |
|  stream  | video stream |     Y     |      | 서버와 연결할 영상 스트림 |

- **응답**

    성공 시 true, 실패 시 false 리턴

## 미디어 서버에 영상 수신

{% code title="index.js" %}
```javascript
//미디어 서버로 stream 수신 요청
await knowledgetalk.subscribeVideo('kpoint', 'cam')
```
{% endcode %}
    
- **요청**

| 파라미터 |  타입  | 필수 여부 |  예시  |       설명        |
| :------: | :----: | :-------: | :----: | :---------------: |
|  userId  | string |     Y     | kpoint |  상대방 USER ID   |
|   type   | string |     Y     |  cam   | cam / screen 구분 |

- **응답**

  성공 시 상대방 video stream 리턴, 실패 시 false 리턴

## P2P 영상 전송

{% code title="index.js" %}
```javascript
//상대방에 stream 전송
await knowledgetalk.publishP2P('kpoint','cam', stream);
```

- **요청**

| 파라미터 |     타입     | 필수 여부 |  예시  |            설명            |
| :------: | :----------: | :-------: | :----: | :------------------------: |
|  userId  |    string    |     Y     | kpoint | 영상을 받을 상대방 USER ID |
|   type   |    string    |     Y     |  cam   |     cam / screen 구분      |
|  stream  | video stream |     Y     |        |        영상 스트림         |

- **응답**

  성공 시 true, 실패 시 false 리턴


## 영상 변경

{% code title="index.js" %}
```javascript
//로컬 스트림 변경(stream)
await knowledgetalk.changeLocalStream(stream);
```

- **요청**

| 파라미터 |     타입     | 필수 여부 | 예시 |     설명      |
| :------: | :----------: | :-------: | :--: | :-----------: |
|  stream  | video stream |     Y     |      | 새로운 스트림 |

- **응답**

  성공 시 true, 실패 시 false