```
let osc; // Oscilador para generar el sonido
let waveType = "sine"; // Tipo de onda inicial
let freqSlider, ampSlider; // Sliders para frecuencia y amplitud

function setup() {
  createCanvas(400, 300);
  textAlign(CENTER, CENTER);

  // Crear un oscilador
  osc = new p5.Oscillator();
  osc.setType(waveType); // Tipo de onda inicial
  osc.start();
  osc.amp(0); // Amplitud inicial en silencio

  // Slider para la frecuencia
  freqSlider = createSlider(100, 1000, 440, 1);
  freqSlider.position(20, height - 80);
  createP("Frecuencia (Hz)").position(20, height - 110);

  // Slider para la amplitud
  ampSlider = createSlider(0, 1, 0.5, 0.01);
  ampSlider.position(20, height - 30);
  createP("Amplitud").position(20, height - 60);

  // Botones para cambiar el tipo de onda
  let sineButton = createButton("Onda Senoidal");
  sineButton.position(280, 80);
  sineButton.mousePressed(() => changeWaveType("sine"));

  let triangleButton = createButton("Onda Triangular");
  triangleButton.position(280, 120);
  triangleButton.mousePressed(() => changeWaveType("triangle"));

  let squareButton = createButton("Onda Cuadrada");
  squareButton.position(280, 160);
  squareButton.mousePressed(() => changeWaveType("square"));
}

function draw() {
  background(50);
  fill(255);
  textSize(16);
  text("Frecuencia: " + freqSlider.value() + " Hz", width / 2, height / 2 - 40);
  text("Amplitud: " + ampSlider.value(), width / 2, height / 2);

  // Actualizar frecuencia y amplitud según los sliders
  osc.freq(freqSlider.value());
  osc.amp(ampSlider.value());
}

// Cambiar el tipo de onda
function changeWaveType(type) {
  waveType = type;
  osc.setType(type);
}
```


![image](https://github.com/user-attachments/assets/6ccf64d7-0634-4ecc-a6a7-4abd4664408a)
