### 1. Identifica inputs a simular
Mis dos inputs si o si se tendrian que simular tanto el del sonido como el del movimiento de la hinchada.

### 2. Define método de simulación
¿Usarás random()? ¿Dentro de qué rango?
RT// Sí, pero solo para pruebas rápidas o para simular picos de ruido tipo "¡gol!". random(0, 100) representando el volumen.

¿Usarás noise() para cambios más suaves y orgánicos? ¿Con qué parámetros iniciales?
RT// Sí, noise() es perfecto para simular cambios más suaves y orgánicos, como el típico murmullo creciente de una afición que empieza a cantar.

¿Crearás sliders o botones simples en pantalla para controlar manualmente el valor simulado durante las pruebas?
RT//Sí, totalmente. Son clave para: Probar visualmente el sistema sin micrófono, Controlar manualmente el nivel de “apoyo” y usar durante presentaciones o prototipos en vivo.

¿Seguirás alguna curva o patrón predefinido?
RT// No ya que para que sea una simulacion verdadera de un estadio, nesecito aleatoriedad.

### 3 Comportamiento simulado
En la simulacion busco cambios repentinos y bruscos, por ejemplo cuando hay un gol o una falta en un partido, no se que sean suaves ya que asi no es un estadio de verdad.
