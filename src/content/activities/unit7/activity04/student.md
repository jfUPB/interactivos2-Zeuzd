## Inputs:
![image](https://github.com/user-attachments/assets/e47a5c61-bd76-40b9-a270-c47180cf96ef)

Los sliders o el simulador generan los valores de volumenA y volumenB. Este input afecta directamente al estado interno del algoritmo.

## Outputs:
![image](https://github.com/user-attachments/assets/def7828e-d73b-4485-93ad-087c888c19c9)

La visualización de barras (output gráfico) depende del volumen actual (estado interno).

## Prototipo en accion:
![20250507-0201-06 2994754](https://github.com/user-attachments/assets/72569f66-6368-430a-aaf1-7d2fb2fc7270)

## Flujo IPO:

En mi sistema, el modelo IPO se refleja claramente: las entradas provienen de sliders, simulación automática o micrófono. Estas entradas modifican el proceso, que calcula niveles de volumen, porcentajes y puntos extra en tiempo real. Luego, el sistema genera salidas visuales (barras, textos) y envía datos al servidor. Así, cualquier cambio en los inputs se traduce dinámicamente en la visualización y comunicación. El flujo garantiza interactividad y retroalimentación continua.
