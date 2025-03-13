```
let words = ["luz", "sueño", "mar", "viento", "alma", "cielo", "camino", "silencio", "esperanza", "sombra"]; // Conjunto de palabras

function setup() {
  createCanvas(800, 800);
  background(30); // Fondo oscuro
  textAlign(CENTER, CENTER); // Centrar texto
  textFont("Georgia"); // Usar la fuente estándar Georgia
  noLoop(); // Detener el loop automático

  generatePoem(); // Generar poema
}

function generatePoem() {
  fill(255); // Color del texto
  textSize(32); // Tamaño de texto

  for (let i = 0; i < 5; i++) { // Generar 5 líneas
    let line = ""; 
    for (let j = 0; j < 4; j++) { // Cada línea tiene 4 palabras
      line += random(words) + " "; // Elegir palabras aleatorias
    }
    text(line.trim(), width / 2, 100 + i * 50); // Dibujar línea
  }
}
```

![image](https://github.com/user-attachments/assets/e6adfe98-3c35-4b47-87c1-03376b4136d9)

