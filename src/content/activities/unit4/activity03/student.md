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
let incomingVideo;

function setup() {
  createCanvas(640, 480);
  
  video = createCapture(VIDEO);
  video.size(640, 480);
  video.hide();
  
  prevFrame = createImage(640, 480);
  colorMode(HSB, 360, 100, 100); // Para manipular saturación

  liveMedia = new p5LiveMedia(this, "CAPTURE", video, "sala-movimiento");
  liveMedia.on("stream", gotStream);
}

function draw() {
  background(0);
  
  video.loadPixels();
  prevFrame.loadPixels();

  let sum = 0;
  
  for (let i = 0; i < video.pixels.length; i += 4) {
    let diff = abs(video.pixels[i] - prevFrame.pixels[i]); // Diferencia en rojo
    sum += diff;
  }
  
  motionAmount = sum / (video.pixels.length / 4);
  
  saturationLevel = map(motionAmount, 0, 50, 0, 100, true);

  drawWithSaturation(video, saturationLevel);

  prevFrame.copy(video, 0, 0, video.width, video.height, 0, 0, video.width, video.height);
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

function gotStream(stream) {
  incomingVideo = createVideo(stream);
  incomingVideo.size(320, 240);
  incomingVideo.position(650, 50);
  incomingVideo.show();
}

```
