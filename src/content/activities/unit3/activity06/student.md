![image](https://github.com/user-attachments/assets/e837eeee-7498-47a9-b513-d9166376eed8)


### Codigo Server:

```
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.on('message', (message) => {
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
io.on('connection', (socket) => {
    console.log('New client connected');

    socket.on('message', (message) => {
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('image', (imgData) => {
        console.log('Received an image');
        socket.broadcast.emit('image', imgData);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});
```

### Codigo Desktop:

```
let socket;
let circleX = 200;
let circleY = 200;
let receivedImg = null;

function setup() {
    createCanvas(400, 400);
    background(220);

    let socketUrl = 'https://obscure-space-guacamole-q5pg4q75rppcxqj-3000.app.github.dev/';
    socket = io(socketUrl);

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
        let parsedData = JSON.parse(data);
        if (parsedData.type === 'touch') {
            circleX = parsedData.x;
            circleY = parsedData.y;
        }
    });

    socket.on('image', (imgData) => {
        console.log('Received image');
        receivedImg = loadImage(imgData); // Convertir Base64 a imagen
    });

    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });
}

function draw() {
    background(220);
    
    if (receivedImg) {
        image(receivedImg, 0, 0, width, height);
    } else {
        fill(255, 0, 0);
        ellipse(circleX, circleY, 50, 50);
    }
}
```

### Codigo Mobile:

```
let socket;
const port = 3000;
let lastTouchX = null; 
let lastTouchY = null; 
const threshold = 5;
let imgData = null;

function setup() {
    createCanvas(400, 400);
    background(220);

    let socketUrl = 'https://obscure-space-guacamole-q5pg4q75rppcxqj-3000.app.github.dev/';
    socket = io(socketUrl);

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
    });

    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });

    // Botón para capturar imagen desde la cámara
    let captureButton = createButton('Capturar imagen');
    captureButton.position(10, height + 10);
    captureButton.mousePressed(captureImage);

    // Botón para cargar imagen desde archivos
    let uploadInput = createFileInput(handleFile);
    uploadInput.position(150, height + 10);
}

function draw() {
    background(220);
    fill(0, 255, 0);
    textAlign(CENTER, CENTER);
    textSize(18);
    text('Toca para mover el círculo\n o envía una imagen', width / 2, height / 2);
}

function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', JSON.stringify(touchData));

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}

// Captura una imagen desde la cámara
function captureImage() {
    let video = createCapture(VIDEO);
    video.size(400, 300);
    video.hide();

    setTimeout(() => {
        image(video, 0, 0, width, height);
        imgData = canvas.toDataURL(); // Convertir imagen a Base64
        socket.emit('image', imgData);
        video.remove();
    }, 2000); // Esperar 2 segundos para la captura
}

// Manejar carga de archivo desde el sistema de archivos
function handleFile(file) {
    if (file.type === 'image') {
        imgData = file.data;
        socket.emit('image', imgData);
    }
}
```


