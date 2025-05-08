## Error:

Si el volumen simulado o detectado supera los límites esperados (por ejemplo, valores negativos o muy superiores a 100), las barras visuales podrían salirse del canvas o no renderizarse correctamente. Esto se debe a que no hay una validación explícita que limite los valores de entrada, lo cual podría generar una distorsión en la visualización o incluso errores en el envío de datos al servidor.

## Console.Log:

Utilicé console.log() tanto en el cliente (sketch.js) como en el servidor (server.js). En el cliente, imprimí los valores de volumenA y volumenB justo antes de enviarlos al servidor y antes de dibujar las barras, lo cual me permitió ver si estaban fuera del rango esperado (por ejemplo, mayores a 100 o negativos). En el servidor, usé console.log() para verificar qué datos estaban llegando realmente mediante los eventos de socket.on. Esto me ayudó a confirmar que el problema no era de la red, sino que los valores calculados en el frontend a veces excedían los límites, afectando la visualización.

## Cambio explicado:
Se corrigió un problema en el que los valores de volumen simulados podían superar el 100%, lo que causaba desbordes visuales en las barras del gráfico. Para solucionarlo, se utilizó la función `constrain()` en p5.js, que limita los valores generados por `map()` al rango permitido (0 a 100). Esto asegura que la visualización se mantenga dentro de los límites esperados y evita errores al calcular porcentajes y representar los datos en pantalla.

## Estetica

Cambie un pedazo de la estetica de las barras de las hinchadas, solo para que se vieran mejor y no simplemente dos barras.

![image](https://github.com/user-attachments/assets/159f625b-6c6d-4e63-80e4-dba5a2332e11)
