Actividad 9

Genera una composición visual aleatoria en p5.js dibujando 50 figuras geométricas (círculos, cuadrados y triángulos) con posiciones, tamaños y colores aleatorios sobre un fondo oscuro.

Análisis
Lo que funciona bien:
Generación dinámica de formas con variedad visual.
Distribución equilibrada de elementos en el lienzo.
Uso eficiente de random() para variedad de colores y tamaños.

Mejoras posibles:
Agregar interacción para regenerar la composición con un clic.
Implementar transparencias y superposiciones para mayor profundidad.
Experimentar con distribuciones menos aleatorias para mejorar la estética.

Aprendizaje y dificultades
Uso de estructuras condicionales para elegir figuras aleatorias.
Creación de funciones auxiliares (drawTriangle()) para modularidad.
La distribución podría optimizarse para evitar solapamientos excesivos.

Actividad 10

Actividad 11

Genera un poema aleatorio en p5.js seleccionando palabras de una lista predefinida y mostrándolas en un fondo oscuro con una fuente elegante.

Análisis
Lo que funciona bien:
Generación aleatoria de versos con variedad visual.
Distribución ordenada del texto en el lienzo.
Uso de noLoop() para evitar redibujados innecesarios.

Mejoras posibles:
Agregar interacción para generar nuevos poemas con un clic.
Usar diferentes tamaños o estilos de fuente para mayor dinamismo.
Implementar animaciones sutiles en la aparición del texto.

Aprendizaje y dificultades
Uso de random(words) para generar combinaciones creativas.
La distribución del texto podría mejorarse con espaciado dinámico.
La estructura del poema es fija; se podría hacer más flexible.

Actividad 12

Carga y muestra una imagen en un lienzo de p5.js, aplicando un efecto de inversión de colores mediante manipulación de píxeles.

Análisis
Lo que funciona bien:
Carga y renderizado correcto de imágenes.
Manipulación de píxeles para efectos visuales.
Optimización con noLoop() para evitar recargas innecesarias.

Mejoras posibles:
Corregir el cálculo del índice de píxeles (index debe ser (x + y * width) * 4).
Permitir aplicar diferentes filtros de imagen.
Agregar interacción para alternar efectos en tiempo real.

Aprendizaje y dificultades
Uso de loadPixels() y updatePixels().
Error en el índice de píxeles que afecta la manipulación.
La imagen puede no cargar si la URL no es accesible.

Actividad 13

Permite ajustar la frecuencia y amplitud mediante sliders y cambiar el tipo de onda (senoidal, triangular y cuadrada) con botones.

Análisis
Lo que funciona bien:
Generación de sonido en tiempo real con p5.Oscillator().
Controles intuitivos para modificar parámetros.
Cambio dinámico del tipo de onda.

Mejoras posibles:
Agregar una opción para detener el sonido.
Mejorar la interfaz visual.
Incluir una representación gráfica de la onda.

Aprendizaje y dificultades
Uso de p5.Oscillator() y controles de UI en p5.js.
Inicialmente, el oscilador sonaba automáticamente.
Ajustar la disposición de los elementos tomó tiempo.

