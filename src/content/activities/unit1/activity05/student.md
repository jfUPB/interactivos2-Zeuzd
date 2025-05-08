#### Codigo 1
``` js
var tileCount = 20;

var moduleColor;
var moduleAlpha = 180;
var maxDistance = 500;

function setup() {
  createCanvas(600, 600);
  noFill();
  strokeWeight(3);
  moduleColor = color(0, 0, 0, moduleAlpha);
}

function draw() {
  clear();

  stroke(moduleColor);

  for (var gridY = 0; gridY < width; gridY += 25) {
    for (var gridX = 0; gridX < height; gridX += 25) {
      var diameter = dist(mouseX, mouseY, gridX, gridY);
      diameter = diameter / maxDistance * 40;
      push();
      translate(gridX, gridY, diameter * 5);
      rect(0, 0, diameter, diameter); // also nice: ellipse(...)
      pop();
    }
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}
```

Este codigo lo que hace es crear una malla la cual cambia de tamaño con respecto a la distancia del mouse respecto a cada rectangulo.

``` js
var tileCount = 20;

var moduleAlpha = 180;
var maxDistance = 500;

function setup() {
  createCanvas(600, 600);
  noFill();
  strokeWeight(3);
}

function draw() {
  clear();

  for (var gridY = 0; gridY < width; gridY += 25) {
    for (var gridX = 0; gridX < height; gridX += 25) {
      var diameter = dist(mouseX, mouseY, gridX, gridY);
      diameter = diameter / maxDistance * 40;

      // Cambio de color dinámico
      var dynamicColor = color(
        map(gridX, 0, width, 0, 255), 
        map(gridY, 0, height, 0, 255), 
        map(diameter, 0, 40, 255, 0), 
        moduleAlpha
      );
      stroke(dynamicColor);

      // Cambiar de rectángulo a círculo
      ellipse(gridX, gridY, diameter, diameter);
    }
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas('generative-art', 'png');
}
```

Ahora se le aplicaron dos cambios al mismo codigo, ahora en vez de ser de cuadrados la malla, es de circulos y en vez de ser negros todos, ahora son de colores.

Esto se puede dar en el entretenimiento digital para darle vida a las obras y para poder controlar las emociones que queremos reflejar, ya que los colores reflejan emociones.

#### Codigo 2

``` js
var tileCountX = 50;
var tileCountY = 10;

var hueValues = [];
var saturationValues = [];
var brightnessValues = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();

  // init with random values
  for (var i = 0; i < tileCountX; i++) {
    hueValues[i] = random(360);
    saturationValues[i] = random(100);
    brightnessValues[i] = random(100);
  }
}

function draw() {
  // white back
  background(0, 0, 100);

  // limit mouse coordinates to canvas
  var mX = constrain(mouseX, 0, width);
  var mY = constrain(mouseY, 0, height);

  // tile counter
  var counter = 0;

  // map mouse to grid resolution
  var currentTileCountX = int(map(mX, 0, width, 1, tileCountX));
  var currentTileCountY = int(map(mY, 0, height, 1, tileCountY));
  var tileWidth = width / currentTileCountX;
  var tileHeight = height / currentTileCountY;

  for (var gridY = 0; gridY < tileCountY; gridY++) {
    for (var gridX = 0; gridX < tileCountX; gridX++) {
      var posX = tileWidth * gridX;
      var posY = tileHeight * gridY;
      var index = counter % currentTileCountX;

      // get component color values
      fill(hueValues[index], saturationValues[index], brightnessValues[index]);
      rect(posX, posY, tileWidth, tileHeight);
      counter++;
    }
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (key == 'c' || key == 'C') {
    // -- save an ase file (adobe swatch export) --
    var colors = [];
    for (var i = 0; i < hueValues.length; i++) {
      colors.push(color(hueValues[i], saturationValues[i], brightnessValues[i]));
    }
    writeFile([gd.ase.encode(colors)], gd.timestamp(), 'ase');
  }

  if (key == '1') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = random(100);
      brightnessValues[i] = random(100);
    }
  }

  if (key == '2') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = random(100);
      brightnessValues[i] = 100;
    }
  }

  if (key == '3') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = 100;
      brightnessValues[i] = random(100);
    }
  }

  if (key == '4') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = 0;
      saturationValues[i] = 0;
      brightnessValues[i] = random(100);
    }
  }

  if (key == '5') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = 195;
      saturationValues[i] = 100;
      brightnessValues[i] = random(100);
    }
  }

  if (key == '6') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = 195;
      saturationValues[i] = random(100);
      brightnessValues[i] = 100;
    }
  }

  if (key == '7') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(180);
      saturationValues[i] = random(80, 100);
      brightnessValues[i] = random(50, 90);
    }
  }

  if (key == '8') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(180, 360);
      saturationValues[i] = random(80, 100);
      brightnessValues[i] = random(50, 90);
    }
  }

  if (key == '9') {
    for (var i = 0; i < tileCountX; i++) {
      if (i % 2 == 0) {
        hueValues[i] = random(360);
        saturationValues[i] = 100;
        brightnessValues[i] = random(100);
      } else {
        hueValues[i] = 195;
        saturationValues[i] = random(100);
        brightnessValues[i] = 100;
      }
    }
  }

  if (key == '0') {
    for (var i = 0; i < tileCountX; i++) {
      if (i % 2 == 0) {
        hueValues[i] = 140;
        saturationValues[i] = random(30, 100);
        brightnessValues[i] = random(40, 100);
      } else {
        hueValues[i] = 210;
        saturationValues[i] = random(40, 100);
        brightnessValues[i] = random(50, 100);
      }
    }
  }

}
```

Este codigo lo que hace es agarrar la posicion del mouse y dependiendo de este, agarras los tiles y expandir el numero de estos hacia los lados y de arriba para abajo.

``` js
var tileCountX = 50;
var tileCountY = 10;

var hueValues = [];
var saturationValues = [];
var brightnessValues = [];
var alphaValues = []; // Nueva variable para la opacidad

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();

  // Inicialización con valores aleatorios
  for (var i = 0; i < tileCountX; i++) {
    hueValues[i] = random(360);
    saturationValues[i] = random(100);
    brightnessValues[i] = random(100);
    alphaValues[i] = random(50, 100); // Opacidad aleatoria
  }
}

function draw() {
  // Fondo blanco
  background(0, 0, 100);

  // Limitar las coordenadas del mouse al lienzo
  var mX = constrain(mouseX, 0, width);
  var mY = constrain(mouseY, 0, height);

  // Contador de tiles
  var counter = 0;

  // Mapear el mouse para cambiar el tamaño de las celdas
  var currentTileCountX = int(map(mX, 0, width, 5, tileCountX)); // Mínimo 5 divisiones
  var currentTileCountY = int(map(mY, 0, height, 2, tileCountY)); // Mínimo 2 divisiones
  var tileWidth = map(mouseX, 0, width, 5, width / currentTileCountX); // Tamaño dinámico
  var tileHeight = map(mouseY, 0, height, 5, height / currentTileCountY); // Tamaño dinámico

  for (var gridY = 0; gridY < currentTileCountY; gridY++) {
    for (var gridX = 0; gridX < currentTileCountX; gridX++) {
      var posX = tileWidth * gridX;
      var posY = tileHeight * gridY;
      var index = counter % hueValues.length;

      // Obtener componentes de color con opacidad
      fill(hueValues[index], saturationValues[index], brightnessValues[index], alphaValues[index]);
      rect(posX, posY, tileWidth, tileHeight);
      counter++;
    }
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas('generative-art', 'png');
  if (key == 'r' || key == 'R') {
    // Reiniciar colores y opacidad
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = random(100);
      brightnessValues[i] = random(100);
      alphaValues[i] = random(50, 100);
    }
  }
}
```

Ahora con los cambios, al mover el mouse, el tamaño de las celdas ahora cambia dinámicamente, no solo la cantidad de divisiones y ahora tiene una transparencia aleatoria a los colores de las celdas.

Este código podría ser utilizado en el entretenimiento digital para crear experiencias interactivas visuales, como arte generativo en videojuegos, instalaciones artísticas o interfaces dinámicas. Al permitir que los patrones de color y forma cambien con el movimiento del mouse, ofrece una respuesta visual atractiva, ideal para juegos o experiencias inmersivas.

#### Codigo 3

``` js
function setup() {
  createCanvas(400, 400);
  colorMode(HSB);

  // Set angle mode so that atan2() returns angles in degrees
  angleMode(DEGREES);

  describe('Two eyes that follow the cursor.');
}

function draw() {
  background(0);

  // Draw left eye

  let leftX = 150;
  let leftY = 200;

  // Calculate angle between left eye and mouse
  let leftAngle = atan2(mouseY - leftY, mouseX - leftX);

  push();
  translate(leftX, leftY);
  fill(255);
  ellipse(0, 0, 50, 50);
  rotate(leftAngle);
  fill(0);
  ellipse(12.5, 0, 25, 25);
  pop();

  // Draw right eye

  let rightX = 250;
  let rightY = 200;

  // Calculate angle between right eye and angle
  let rightAngle = atan2(mouseY - rightY, mouseX - rightX);

  push();
  translate(rightX, rightY);
  fill(255);
  ellipse(0, 0, 50, 50);
  rotate(rightAngle);
  fill(0);
  ellipse(12.5, 0, 25, 25);
  pop();
}
```

Este código tiene dos ojos que siguen la direccion del mouse.

``` js
let blinkTimer = 0; // **Cambio 1**: Temporizador para parpadeo aleatorio

function setup() {
  createCanvas(400, 400);
  colorMode(HSB);

  // Set angle mode so that atan2() returns angles in degrees
  angleMode(DEGREES);

  describe('Two eyes that follow the cursor and blink randomly.');
}

function draw() {
  // **Cambio 2**: Color de fondo dinámico basado en el mouse
  background(map(mouseX, 0, width, 0, 360), 100, 100);

  // Verifica si es momento de parpadear
  let isBlinking = millis() > blinkTimer;

  // Ojo izquierdo
  let leftX = 150;
  let leftY = 200;
  let leftAngle = atan2(mouseY - leftY, mouseX - leftX);

  push();
  translate(leftX, leftY);
  fill(255);
  ellipse(0, 0, 50, isBlinking ? 10 : 50); // Parpadeo
  if (!isBlinking) {
    rotate(leftAngle);
    fill(0);
    ellipse(12.5, 0, 25, 25);
  }
  pop();

  // Ojo derecho
  let rightX = 250;
  let rightY = 200;
  let rightAngle = atan2(mouseY - rightY, mouseX - rightX);

  push();
  translate(rightX, rightY);
  fill(255);
  ellipse(0, 0, 50, isBlinking ? 10 : 50); // Parpadeo
  if (!isBlinking) {
    rotate(rightAngle);
    fill(0);
    ellipse(12.5, 0, 25, 25);
  }
  pop();

  // **Cambio 1**: Restablece el temporizador si los ojos parpadean
  if (isBlinking) {
    blinkTimer = millis() + random(2000, 5000); // Parpadea entre 2 y 5 segundos
  }
}
```

Ahora con estos cambios, el fondo cambia de color en base a la posicion del mouse y los ojos parpadean de vez en cuando.

Este código podría ser utilizado en el entretenimiento digital para crear animaciones interactivas donde los personajes o elementos gráficos reaccionan al movimiento del cursor y a eventos aleatorios.

