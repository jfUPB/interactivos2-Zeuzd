```
function setup() {
  createCanvas(800, 800); // Tamaño del canvas
  noLoop(); // Detener el loop automático para que solo dibuje una vez
}

function draw() {
  background(30); // Fondo oscuro para resaltar las formas
  
  for (let i = 0; i < 50; i++) {
    let shapeType = int(random(3)); // 0: círculo, 1: cuadrado, 2: triángulo
    let x = random(width); // Posición X aleatoria
    let y = random(height); // Posición Y aleatoria
    let size = random(20, 100); // Tamaño aleatorio
    let col = color(random(255), random(255), random(255), random(200, 255)); // Color aleatorio

    fill(col); // Aplicar color de relleno
    noStroke(); // Sin bordes

    if (shapeType === 0) {
      ellipse(x, y, size, size); // Dibuja un círculo
    } else if (shapeType === 1) {
      rect(x, y, size, size); // Dibuja un cuadrado
    } else if (shapeType === 2) {
      drawTriangle(x, y, size); // Dibuja un triángulo
    }
  }
}

function drawTriangle(x, y, size) {
  let halfSize = size / 2;
  triangle(
    x, y - halfSize, // Vértice superior
    x - halfSize, y + halfSize, // Vértice inferior izquierdo
    x + halfSize, y + halfSize // Vértice inferior derecho
  );
}

```

![image](https://github.com/user-attachments/assets/b106bfbb-68ee-4dc3-a772-aeee5166b466)
