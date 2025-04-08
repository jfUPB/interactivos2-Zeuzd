# Blueprint Algorítmico - Unidad 6

###  Resumen: 
Una batalla interactiva de ruido en un estadio, donde dos aficiones compiten en tiempo real con su energía sonora para llenar una pantalla con intensidad y emoción.

### Inputs: 
Sensores de sonido y sensores de movimiento.

### Algoritmo:
Captura de sonido (input):
Se reciben datos de audio desde distintos micrófonos ubicados estratégicamente en cada zona del estadio (por ejemplo, uno por hinchada). Se mide la amplitud o volumen del sonido en tiempo real.

Normalización del volumen:
Las frecuencias captadas se transforman a un valor entre 0 y 1 (o 0% a 100%) para representar el nivel de ruido relativo.

Comparación entre hinchadas:
Cada hinchada tiene su propio medidor. Los niveles normalizados se comparan en tiempo real para mostrar qué hinchada está haciendo más ruido.

Umbrales y bonus:
Se definen umbrales de energía (por ejemplo, 70%, 85%, 95%).
Si una hinchada supera un umbral por un tiempo definido, gana puntos extra o activa un efecto visual (chispas, explosiones, animaciones) que motiva más al público.

Visualización en pantalla:
Todo esto se traduce en una interfaz dinámica

Feedback en tiempo real:
La visualización le dice a la hinchada “¡vas ganando!” o “¡falta más ruido!”, alimentando el entusiasmo y reforzando la participación.

### Outputs:
1. Medidores de ruido (uno por hinchada)
Forma: Barras verticales o circulares.

Rango: Escala de 0% a 100%.

Dinámica:

Se actualizan en tiempo real con lerp() para suavizar.

El color cambia según el nivel (verde < 50%, amarillo 50–85%, rojo > 85%).

Vibran o pulsan cuando se alcanzan picos altos.

2. Porcentaje de energía
Texto grande en pantalla: "Hinchas Norte: 78% – Hinchas Sur: 66%"

Dinámica:

Actualización en tiempo real.

Fuente crece o parpadea cuando hay cambio significativo (>10% en pocos segundos).

3. Puntos acumulados
Visual tipo marcador o contador numérico.

Dinámica:

Se suman puntos cada vez que se cruza un umbral de ruido.

Efecto “+100” flota sobre la hinchada que lo logró.

4. Indicadores de umbrales
Iconos o líneas marcadas a los 70%, 85%, 95%.

Dinámica:

Se iluminan o explotan con efectos visuales cuando se cruzan.

Activan animaciones breves (fuegos artificiales, luces, partículas).

5. Fondo interactivo
Visual generativo detrás de los medidores.

Dinámica:

Cambia según el promedio del ruido total.

Más ruido = más movimiento, color y brillo.

6. Mensaje motivacional
Ej: “¡Hinchas del Norte están arrasando!”

Dinámica:

Aparece automáticamente cuando una hinchada supera por más de 15% a la otra.

Desaparece lentamente si se igualan.
