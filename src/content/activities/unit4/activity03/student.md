Me invente un codigo el cual captura la imagen y compara el fotograma nuevo con el anterior para detectar movimiento y entre mas movimiento haya, mas va a subir la saturacion de los colores.

## .HTML
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.1/p5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.1/addons/p5.sound.min.js"></script>
    
    <!-- Scripts de p5LiveMedia -->
    <script type="text/javascript" src="https://p5livemedia.itp.io/simplepeer.min.js"></script>
    <script type="text/javascript" src="https://p5livemedia.itp.io/socket.io.js"></script>
    <script type="text/javascript" src="https://p5livemedia.itp.io/p5livemedia.js"></script>

    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />
  </head>
  <body>
    <main></main>
    <script src="sketch.js"></script>
  </body>
</html>
```

## .JS
```
let video;
let prevFrame;
let motionAmount = 0;
let saturationLevel = 0;
let liveMedia;

function setup() {
  createCanvas(640, 480);
  
  // Captura de video
  video = createCapture(VIDEO);
  video.size(640, 480);
  video.hide();
  
  // Imagen previa para detectar movimiento
  prevFrame = createImage(640, 480);
  colorMode(HSB, 360, 100, 100); // HSB para controlar la saturación

  // Inicializar p5LiveMedia para enviar y recibir datos
  liveMedia = new p5LiveMedia(this, "DATA", null, "sala-local");
  liveMedia.on("data", gotData);
}

function draw() {
  background(0);
  
  video.loadPixels();
  prevFrame.loadPixels();

  let sum = 0;
  
  // Comparar cada píxel con el cuadro anterior
  for (let i = 0; i < video.pixels.length; i += 4) {
    let diff = abs(video.pixels[i] - prevFrame.pixels[i]); // Diferencia en rojo
    sum += diff;
  }
  
  // Promedio de diferencia
  motionAmount = sum / (video.pixels.length / 4);
  
  // Ajustar la saturación entre 0 y 100 según la cantidad de movimiento
  saturationLevel = map(motionAmount, 0, 50, 0, 100, true);

  // Enviar datos de movimiento y saturación usando p5LiveMedia
  let dataToSend = {
    motion: motionAmount,
    saturation: saturationLevel
  };
  liveMedia.send(JSON.stringify(dataToSend));

  // Dibujar el video con la saturación ajustada
  drawWithSaturation(video, saturationLevel);

  // Guardar el fotograma actual como el anterior para la próxima iteración
  prevFrame.copy(video, 0, 0, video.width, video.height, 0, 0, video.width, video.height);
}

// Recibir datos enviados y actualizar variables (autoenvío)
function gotData(data) {
  let receivedData = JSON.parse(data);
  motionAmount = receivedData.motion;
  saturationLevel = receivedData.saturation;
}

function drawWithSaturation(source, sat) {
  source.loadPixels();
  
  for (let i = 0; i < source.pixels.length; i += 4) {
    let r = source.pixels[i];
    let g = source.pixels[i + 1];
    let b = source.pixels[i + 2];
    
    let c = color(r, g, b);
    let h = hue(c);
    let bval = brightness(c);

    let newColor = color(h, sat, bval);
    
    source.pixels[i] = red(newColor);
    source.pixels[i + 1] = green(newColor);
    source.pixels[i + 2] = blue(newColor);
  }

  source.updatePixels();
  image(source, 0, 0, width, height);
}


```
