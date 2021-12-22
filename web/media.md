# 영상 연결 기능
 
## 미디어 서버에 영상 송신

{% code title="index.js" %}
```javascript
// 미디어 서버에 영상 송신(cam, stream)
await knowledgetalk.publishVideo('cam', stream);
```
{% endcode %}

- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|              type             |           String          |                Y               |       cam / screen 구분       |              cam              |
|             stream            |        video stream       |                Y               |    서버와 연결할 영상 스트림   |                               |

- **응답**

  성공 시 true, 실패 시 false 리턴
 
## 미디어 서버에 영상 수신

{% code title="index.js" %}
```javascript
// 미디어 서버에 영상 수신(userId, cam)
await knowledgetalk.subscribeVideo('kpoint123', 'cam')
```
{% endcode %}
    
- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             userId            |           String          |                Y               |         상대방의 userId        |           kpoint123          |
|              type             |           String          |                Y               |        cam / screen 구분       |              cam             |

- **응답**

  성공 시 상대방 video stream 리턴, 실패 시 false 리턴
 
## P2P 영상 전송

{% code title="index.js" %}
```javascript
// P2P 영상 전송(userId, cam, stream)
await knowledgetalk.publishP2P('kpoint123','cam', stream);
```
{% endcode %}

- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             userId            |           String          |                Y               |   영상을 받을 상대방 USER ID   |            kpoint123          |
|              type             |           String          |                Y               |       cam / screen 구분       |              cam              |
|             stream            |        video stream       |                Y               |          영상 스트림          |                                |

- **응답**

  성공 시 true, 실패 시 false 리턴
 
## 영상 정보 변경

{% code title="index.js" %}
```javascript
// 영상 정보 변경(stream)
await knowledgetalk.changeLocalStream(stream);
```
{% endcode %}

- **요청**

| <center>**파라미터**</center> | <center>**타입**</center> | <center>**필수 여부**</center> |   <center>**설명**</center>   |   <center>**예시**</center>   |
|:-:|:-:|:-:|:-:|:-:|
|             stream            |        video stream       |                Y               |     새로 변경될 영상 스트림     |                               |

- **응답**

  성공 시 true, 실패 시 false