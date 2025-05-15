## Server:
![image](https://github.com/user-attachments/assets/1dfc24a5-2c33-44c7-81c3-ef37e9615e02)

## Sketch:
![image](https://github.com/user-attachments/assets/b320916d-46ab-4ed3-8334-47b2a31ccde0)
![image](https://github.com/user-attachments/assets/af6dba5d-2c45-42cf-9323-615e14dbdc9f)

## Salidas (server y navegador):
![image](https://github.com/user-attachments/assets/b3e8b250-4e79-49dc-8e30-57908e8a4a55)
![image](https://github.com/user-attachments/assets/5b534dc7-5eb6-4471-8e01-adb8920d43ad)

## Flujo

1. El servidor se inicia con Express y Socket.IO y escucha conexiones en el puerto 3000.

2. El cliente se conecta automáticamente al servidor mediante socket = io();.

3. Al conectarse, el servidor emite un mensaje de bienvenida, que el cliente recibe y muestra en la consola del navegador.

4. Al hacer clic con el mouse, el cliente envía un objeto con los datos de volumen simulados al servidor mediante el evento datosSimulados.

5. El servidor escucha ese evento y muestra los datos en la terminal.

6. Cuando el cliente se desconecta, el servidor lo detecta y muestra un mensaje de desconexión.
