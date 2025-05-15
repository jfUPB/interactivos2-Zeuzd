#### Movimiento de Líneas Aleatorias (Generación de Líneas Dinámicas)
```
let lines = [];

function setup() {
  createCanvas(400, 400);
  strokeWeight(2);
}

function draw() {
  background(255);

  // Crear líneas aleatorias
  if (frameCount % 5 == 0) {
    lines.push(new RandomLine(random(width), random(height)));
  }

  // Actualizar y mostrar las líneas
  for (let i = lines.length - 1; i >= 0; i--) {
    lines[i].update();
    lines[i].show();
    if (lines[i].isOffScreen()) {
      lines.splice(i, 1);
    }
  }
}

class RandomLine {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-2, 2), random(-2, 2));
    this.color = color(random(255), random(255), random(255));  // Color aleatorio
  }

  update() {
    this.position.add(this.velocity);
  }

  show() {
    stroke(this.color);
    line(this.position.x, this.position.y, this.position.x + random(-50, 50), this.position.y + random(-50, 50));
  }

  isOffScreen() {
    return this.position.x < 0 || this.position.x > width || this.position.y < 0 || this.position.y > height;
  }
}

```
Este código genera líneas que se dibujan en direcciones aleatorias y se actualizan constantemente, creando un patrón dinámico en la pantalla.

Ajuste en el color: Cambiar cómo se asignan los colores de las líneas. Por ejemplo, si deseas que todas las líneas tengan un color fijo:
```
this.color = color(0, 0, 255);  // Color fijo (azul)
```

Cambio en la velocidad: Modificar la velocidad de las líneas, aumentando el rango de random(-2, 2):
```
this.velocity = createVector(random(-5, 5), random(-5, 5));  // Aumenta la velocidad
```


#### Animación de Partículas
Este código crea partículas que se mueven por la pantalla y reaccionan a la gravedad.

```
let particles = [];

function setup() {
  createCanvas(400, 400);
  noStroke();
}

function draw() {
  background(255);

  // Crear nuevas partículas
  if (frameCount % 2 == 0) {
    particles.push(new Particle(mouseX, mouseY));
  }

  // Actualizar y dibujar las partículas
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].show();
    if (particles[i].isOffScreen()) {
      particles.splice(i, 1);
    }
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 1));
    this.acceleration = createVector(0, 0.1);  // Gravedad
    this.lifespan = 255;
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;  // Desvanecimiento de la partícula
  }

  show() {
    fill(0, this.lifespan);
    ellipse(this.position.x, this.position.y, 10);
  }

  isOffScreen() {
    return this.position.y > height || this.position.x < 0 || this.position.x > width;
  }
}
```

Ajuste de la gravedad: Cambiar la fuerza de la gravedad modificando el valor de this.acceleration en la clase Particle:
```
this.acceleration = createVector(0, 0.2); // Aumenta la gravedad
```

Cambio en el color de las partículas: Puedes hacer que las partículas cambien de color a medida que se mueven. Modifica el color en la función show():
```
fill(map(this.lifespan, 255, 0, 0, 255), this.lifespan);
```

#### Reflexion
El código generativo crea arte dinámico y único utilizando algoritmos. Permite manipular parámetros como color, forma y movimiento, lo que genera resultados variables y creativos cada vez que se ejecuta.
Es muy util a la hora de crear arte dinámico, patrones complejos, animaciones interactivas y visualizaciones personalizadas. Permite producir resultados únicos y adaptativos, lo cual es ideal para proyectos de entretenimiento digital, diseño gráfico y arte interactivo.


