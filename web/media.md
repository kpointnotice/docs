# 영상 연결 기능

## 미디어 서버에 영상 송신

{% code title="index.js" %}

```javascript
// 미디어 서버에 영상 송신(cam, stream)
await knowledgetalk.publishVideo("cam", stream);
```

{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> | <center>**예시**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: | :-----------------------: |
|              type              |          String           |               Y               |        cam / screen 구분         |            cam            |
|             stream             |       video stream        |               Y               |    서버와 연결할 영상 스트림     |                           |

- **응답**

  성공 시 true, 실패 시 false 리턴

## 미디어 서버에 영상 수신

{% code title="index.js" %}

```javascript
// 미디어 서버에 영상 수신(userId, cam)
await knowledgetalk.subscribeVideo("kpoint123", "cam");
```

{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> | <center>**예시**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: | :-----------------------: |
|             userId             |          String           |               Y               |         상대방의 userId          |         kpoint123         |
|              type              |          String           |               Y               |        cam / screen 구분         |            cam            |

- **응답**

  성공 시 상대방 video stream 리턴, 실패 시 false 리턴

## P2P 영상 전송

{% code title="index.js" %}

```javascript
// P2P 영상 전송(userId, cam, stream)
await knowledgetalk.publishP2P("kpoint123", "cam", stream);
```

{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> | <center>**예시**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: | :-----------------------: |
|             userId             |          String           |               Y               |    영상을 받을 상대방 USER ID    |         kpoint123         |
|              type              |          String           |               Y               |        cam / screen 구분         |            cam            |
|             stream             |       video stream        |               Y               |           영상 스트림            |                           |

- **응답**

  성공 시 true, 실패 시 false 리턴

## 피어 종료

{% code title="index.js" %}

```javascript
// 피어 종료(target, type)
await knowledgetalk.removePeer("kpoint123", "cam");
```

{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> | <center>**예시**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: | :-----------------------: |
|             target             |          String           |               Y               |      종료할 피어의 USER ID       |         kpoint123         |
|              type              |          String           |               Y               |        cam / screen 구분         |            cam            |

- **응답**

  성공 시 true, 실패 시 false 리턴

## 영상 정보 변경

{% code title="index.js" %}

```javascript
// 영상 정보 변경(stream, target)
await knowledgetalk.changeLocalStream(stream, target);
```

{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> | <center>**예시**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: | :-----------------------: |
|             stream             |       video stream        |               Y               |     새로 변경될 영상 스트림      |                           |
|             target             |          String           |               Y               |      p2p인 경우 상대방 USER ID       |         kpoint123         |

- **응답**

  성공 시 true, 실패 시 false

## 사생활 보호 시작

{% code title="index.js" %}

```javascript
// 사생활 보호 시작(video tag)
let blurredStream = await knowledgetalk.starBlur(videoElement);
```

{% endcode %}

- **요청**

| <center>**Parameter**</center> | <center>**Type**</center> | <center>**Required**</center> | <center>**Description**</center> | <center>**예시**</center> |
| :----------------------------: | :-----------------------: | :---------------------------: | :------------------------------: | :-----------------------: |
|             videoElement             |          video tag           |               Y               |         video tag          |                  |

- **응답**

  성공 시 사생활 보호처리된 stream 리턴, 실패 시 false


## 사생활 보호 중지

{% code title="index.js" %}

```javascript
// 사생활 보호 중지
knowledgetalk.stopBlur();
```

{% endcode %}

- **응답**

  성공 시 true, 실패 시 false