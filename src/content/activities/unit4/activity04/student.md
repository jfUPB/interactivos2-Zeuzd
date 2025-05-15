WebRTC (Web Real-Time Communication)
WebRTC es una tecnología que permite la comunicación en tiempo real de audio, video y datos entre navegadores y dispositivos sin necesidad de servidores intermedios. Se usa en videollamadas, streaming y aplicaciones colaborativas.

¿Cómo funciona WebRTC?
Descubrimiento y conexión: Se intercambian datos a través de un signaling server.
Intercambio de información ICE: Se usan STUN/TURN servers para determinar la mejor ruta de conexión entre los usuarios.
Conexión entre pares (peer-to-peer): Una vez establecida, los datos fluyen directamente entre los dispositivos.
¿Qué es un Peer Connection?
Es el enlace peer-to-peer que permite la transmisión de audio, video o datos entre dos usuarios usando WebRTC.

¿Qué es un Data Channel?
Es un canal en WebRTC que permite enviar datos arbitrarios (texto, JSON, archivos, etc.) entre pares de manera rápida y segura.

¿Qué es un Media Stream?
Es un flujo de audio y/o video capturado desde la cámara o micrófono y transmitido a través de WebRTC.

¿Qué es un ICE Server?
Son servidores que ayudan a los navegadores a descubrir la mejor manera de conectarse entre sí. Incluyen STUN y TURN servers.

¿Qué es un STUN Server?
Un servidor que permite a los dispositivos descubrir su IP pública y puerto cuando están detrás de un NAT (router). No retransmite datos, solo facilita la conexión directa.

¿Qué es un TURN Server?
Si una conexión directa no es posible (por firewalls o restricciones de red), un TURN server actúa como un retransmisor de datos, asegurando la comunicación entre pares.

¿Qué es un Signaling Server?
Es un servidor que ayuda a los pares a intercambiar información inicial (como direcciones IP y configuración de conexión) antes de establecer la conexión WebRTC.
