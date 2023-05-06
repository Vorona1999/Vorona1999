<!DOCTYPE html>
<html>
<head>
  <title>Chat Roulette</title>
  <style>
    body {
      background-color: #0080ff;
    }
    #video-container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 500px;
    }
    video {
      margin: 0 10px;
      border-radius: 8px;
      background-color: white;
    }
    #buttons-container {
      display: flex;
      justify-content: center;
      margin-top: 20px;
    }
    button {
      padding: 10px 20px;
      border-radius: 8px;
      background-color: white;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      margin: 0 10px;
    }
    /* CSS для размещения логотипа по центру экрана */
    #logo {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      margin-top: 5px;
    }
    #my-image {
      margin-top: 200px;
      margin-bottom: 100px;
    }
    .image-container img {
      margin-top: -1500px;
    }

    .image-container {
      margin: 100px auto; /* устанавливаем отступы сверху и снизу, и центрируем элемент по горизонтали */
      animation: up-down 2s linear infinite; /* применяем анимацию */
      margin-left: 260px; /* перемещаем изображение на 20 пикселей вправо */
    }

    @keyframes up-down {
      0% { transform: translateY(0); } /* изначальное положение */
      50% { transform: translateY(-20px); } /* положение в середине анимации */
      100% { transform: translateY(0); } /* положение в конце анимации */
    }
  </style>
  <link rel="icon" type="image/png" href="/images/favicon.png">
</head>
<body>
  <div id="logo">
    <img src="your_logo.png" alt="VideoMask">
  </div>

  <div id="video-container">
    <video id="my-video" width="420" height="340" autoplay muted playsinline></video>
    <video id="peer-video" width="420" height="340"></video>
  </div>

  <div id="buttons-container">
    <button id="start-call-btn" onclick="startCall()">Старт</button>
    <button id="next-call-btn" onclick="nextCall()" disabled>Далее</button>
    <button id="end-call-btn" onclick="endCall()" >Завершить</button>
  </div>

  

<script src="https://cdnjs.cloudflare.com/ajax/libs/peerjs/1.3.2/peerjs.min.js" integrity="sha512-vevmkjYdI4bD+sOv4nBQktT15K7TVn4esmSQD6mJZ/8D3CgOpZV2ulAkOtJipZR51eK2sR6qz30b1B6lNnNfnw==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

<script>
  // Импортируем библиотеку PeerJS и создаем новый объект Peer
  const peer = new Peer();

  // Функция для подключения к серверу PeerJS и получения идентификатора пользователя
  peer.on('open', function (id) {
    console.log('My peer ID is: ' + id);
  });

  // Функция для подключения к другому пользователю
  function connectToPeer() {
    // Получаем ID другого пользователя
    const peerId = document.getElementById('peer-id-input').value;
    // Проверяем, что значение peerId не пустое
    if (!peerId) {
      console.log('Peer ID is empty');
      return;
    }
    // Создаем новое соединение с другим пользователем
    const conn = peer.connect(peerId);
    // Обрабатываем событие открытия соединения
    conn.on('open', function() {
      console.log('Connected to peer ' + peerId);
      // Отправляем сообщение о начале звонка
      conn.send({type: 'call-start'});
    });
    // Обрабатываем событие ошибки
    conn.on('error', function(err) {
      console.log('Connection error:', err);
    });
  }

  // Функция для начала звонка
  async function startCall() {
    try {
      // Получаем поток с камеры
      const stream = await navigator.mediaDevices.getUserMedia({ video: true });
      // Запускаем видео в левом окошке
      const myVideoElement = document.getElementById('my-video');
      myVideoElement.srcObject = stream;
      // Получаем ID другого пользователя
      const peerId = document.getElementById('peer-id-input').value;
      // Создаем новый объект PeerConnection
      const peerConnection = new RTCPeerConnection();
      // Добавляем поток в PeerConnection
      stream.getTracks().forEach(function(track) {
        peerConnection.addTrack(track, stream);
      });

      // Обрабатываем событие получения ICE-кандидата
      peerConnection.onicecandidate = (event) => {
        if (event.candidate) {
          // Если есть ICE-кандидат, отправляем его второй стороне
          sendMessage({
            type: "candidate",
            candidate: event.candidate,
          });
        }
      };

      // Обрабатываем событие успешного добавления удаленного потока
      peerConnection.ontrack = (event) => {
        // Показываем видео от удаленного пользователя в элементе video
        const remoteVideo = document.getElementById('remote-video');
        remoteVideo.srcObject = event.streams[0];
      };

      // Создаем новое соединение WebSocket
      const websocket = new WebSocket('ws://localhost:9000');

      // Обрабатываем событие открытия соединения WebSocket
      websocket.onopen = () => {
        console.log('WebSocket connection opened');
        // Создаем предложение для другого пользователя
        peerConnection.createOffer().then(function(offer) {
          // Устанавливаем локальное описание соединения
          peerConnection.setLocalDescription(offer);
          // Отправляем предложение
          websocket .send(JSON.stringify({
            type: 'offer',
            offer: offer,
            peerId: peerId,
          }));
        });
      };

      // Обрабатываем событие получения сообщения по WebSocket
      websocket.onmessage = (event) => {
        const message = JSON.parse(event.data);
        switch (message.type) {
          case 'offer':
            // Получаем предложение от другого пользователя
            peerConnection.setRemoteDescription(new RTCSessionDescription(message.offer));
            // Создаем ответное предложение
            peerConnection.createAnswer().then(function(answer) {
              // Устанавливаем локальное описание соединения
              peerConnection.setLocalDescription(answer);
              // Отправляем ответное предложение
              websocket.send(JSON.stringify({
                type: 'answer',
                answer: answer,
                peerId: message.peerId,
              }));
            });
            break;
          case 'answer':
            // Получаем ответное предложение от другого пользователя
            peerConnection.setRemoteDescription(new RTCSessionDescription(message.answer));
            break;
          case 'candidate':
            // Добавляем ICE-кандидата
            peerConnection.addIceCandidate(new RTCIceCandidate(message.candidate));
            break;
          default:
            console.log('Unknown message type:', message.type);
        }
      };

      // Обрабатываем событие ошибки
      websocket.onerror = (error) => {
        console.error('WebSocket error:', error);
      };

      console.log('Call started');
    } catch (error) {
      console.error('Failed to start call:', error);
    }
  }
  // Функция для завершения звонка
function endCall() {
  // Остановить поток с камеры
  const stream = myVideoElement.srcObject;
  stream.getTracks().forEach(function(track) {
    track.stop();
  });
}
  // Закрыть соединение WebSocket
  websocket.close();
  // Закрыть соединение PeerConnection
  peerConnection.close();

  // Обнуляем переменные
  myVideoElement = null;
  peerConnection = null;
  websocket = null;
}

// Функция для отправки текстового сообщения
function sendMessage(message) {
  // Отправить сообщение через соединение PeerJS
  conn.send(message);
}

// Обработчик события отправки текстового сообщения
document.getElementById('send-message-button').addEventListener('click', function() {
  const messageInput = document.getElementById('message-input');
  const message = messageInput.value;
  // Отправить сообщение другому пользователю
  sendMessage({type: 'message', text: message});
  // Очистить поле ввода
  messageInput.value = '';
});

// Обработчик события получения текстового сообщения
conn.on('data', function(data) {
  if (data.type === 'message') {
    const messageBox = document.getElementById('message-box');
    const messageElement = document.createElement('div');
    messageElement.textContent = data.text;
    messageBox.appendChild(messageElement);
  }
});
// Обработчик события ошибки
peerConnection.onerror = (error) => {
  console.error('PeerConnection error:', error);
};

// Обработчик события ошибки getUserMedia
navigator.mediaDevices.getUserMedia({ video: true }).catch((error) => {
  console.error('getUserMedia error:', error);
});

// Обработчик события ошибки соединения PeerJS
peer.on('error', function (error) {
  console.error('PeerJS error:', error);
});

</script>
</body>
</html>

