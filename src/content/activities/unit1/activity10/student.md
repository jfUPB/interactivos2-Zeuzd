http://www.generative-gestaltung.de/2/sketches/?01_P/P_1_0_01

```
function setup() {
  createCanvas(600, 600);
}

function draw() {
  let size = map(mouseX, 0, width, 50, 300); // Tamaño del cuadrado
  let bgColor = map(mouseY, 0, height, 0, 255); // Color del fondo
  let squareColor = 255 - bgColor; // Color del cuadrado (contraste)

  background(bgColor);
  fill(squareColor);
  rectMode(CENTER);
  rect(width / 2, height / 2, size, size);
}
```
