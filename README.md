theremi digital con arduino uno hardware digitaj
Descricion del proyecto
este proyecto consiste en le desarrollo y validacion de un theremi digital interactivo en la plataforma de arduino uno. El instrumentomusical
opera sin contacto físico, utilizando un sensor de distancia ultrasónico (HC-SR04) para medir la posición de la mano del usuario y traducir esa
distancia en un tono audible emitido por un zumbador pasivo.
Además, el sistema integra tres pulsadores con configuración de resistencia interna ⁠INPUT_PULLUP⁠ para seleccionar en tiempo real entre tres registros
o rangos tonales (Grave, Medio y Agudo).

2. Componentes Utilizados y Especificaciones
 Arduino UNO R3 (1 unidad): Microcontrolador ATmega328P. Funciona como la unidad central de procesamiento y control.
 Sensor Ultrasónico HC-SR04 (1 unidad): Sensor de 5V. Mide la distancia de la mano al sensor.
 Zumbador Pasivo (1 unidad): Buzzer de 5V. Emite la señal acústica variable mediante la función ⁠tone()⁠.
 Pulsadores / Push Buttons (3 unidades): Switches SPST. Permiten la selección del rango tonal (Grave, Medio, Agudo).
 Protoboard (1 unidad): Placa de pruebas estándar para el montaje del circuito.
 Cables Jumpers (Varios): Conectores Macho-Macho / Macho-Hembra para la interconexión de componentes y alimentación.

3. Esquema y Diagrama de Conexiones
El cableado y la asignación de pines digitales en el Arduino UNO se estructuran de la siguiente forma:
 Pulsadores de Selección de Rango:
 Pulsador Grave: Pin digital 2 \rightarrow Conectado a GND (uso de ⁠INPUT_PULLUP⁠).
 Pulsador Medio: Pin digital 3 \rightarrow Conectado a GND (uso de ⁠INPUT_PULLUP⁠).
 Pulsador Agudo: Pin digital 4 \rightarrow Conectado a GND (uso de ⁠INPUT_PULLUP⁠).
 Sensor Ultrasónico (HC-SR04):
 VCC: Riel positivo 5V de la protoboard.
 GND: Riel negativo GND de la protoboard.
 Trig (Disparo): Pin digital 7 del Arduino.
 Echo (Eco): Pin digital 8 del Arduino.
 Zumbador Pasivo (Buzzer):
 Terminal positivo (+): Pin digital 9 del Arduino.
 Terminal negativo (-): Riel negativo GND de la protoboard.

4. Rangos Tonales y Frecuencias
   
El sistema asigna una octava completa a cada registro tonal seleccionado:
 Rango Grave: Frecuencia de 131 Hz a 262 Hz (Referencia musical: Do3 a Do4).
 Rango Medio: Frecuencia de 262 Hz a 523 Hz (Referencia musical: Do4 a Do5).
 Rango Agudo: Frecuencia de 523 Hz a 1047 Hz (Referencia musical: Do5 a Do6).


 

5. Explicación de la lógica del firmware
   
El código está dividido en varias funciones, donde cada una cumple una tarea específica. La idea es que el instrumento responda
rápidamente a los movimientos de la mano y pueda cambiar el sonido sin interrupciones.
1. Lectura de botones (leerBotones)
El sistema utiliza tres botones para seleccionar los diferentes rangos de sonido. Cuando se presiona uno, el programa detecta cuál
 fue y actualiza el rango seleccionado. También tiene un sistema antirrebote que evita que una sola pulsación se registre varias veces.
 Para esto, utiliza la función millis() en vez de delay(), permitiendo que el programa siga funcionando mientras espera.
2. Medición de distancia (medirDistancia)
El sensor ultrasónico mide la distancia entre la mano y el instrumento. Para hacerlo, envía una señal y espera a que vuelva el eco. Con el
 tiempo que demora en regresar, calcula la distancia en centímetros. Si la mano está demasiado cerca, demasiado lejos o no se recibe una respuesta
 válida, el programa considera que la medición no sirve.
3. Filtrado de la señal (filtrar)
A veces, el sensor entrega mediciones que cambian mucho, aunque la mano casi no se mueva. Para evitarlo, el programa utiliza un promedio de las
 últimas cinco mediciones. Así, la distancia es más estable y el sonido no cambia bruscamente.
4. Cálculo de frecuencia y generación del sonido (calcularFrecuencia y actualizarSonido)
Con la distancia medida, el programa calcula qué frecuencia debe emitir el zumbador. Cada botón permite trabajar con un rango de sonidos
diferente: grave, medio o agudo. Además, la frecuencia cambia según la posición de la mano: mientras más cerca esté, más agudo será el sonido.
 Finalmente, el programa utiliza tone() para generar el sonido y noTone() para silenciarlo cuando la mano está fuera del rango de detección.



6 Instrucciones para compilar y cargar desde vs code 
1 Clonar el Repositorio desde GitHub:
Abre una terminal en tu computador o dentro de VS Code y ejecuta:
2 Abrir el Proyecto en VS Code:
* Abre VS Code.
* Ve a Archivo → Abrir carpeta... (File -> Open
Folder) y selecciona la carpeta del proyecto descargado (tarea_2).
3. Conectar la Placa:
* Conecta tu placa Arduino UNO al computador utilizando el cable USB.
4
Compilar el Proyecto:
* Con PlatformIO: Haz clic en el icono de marca de verificación (Build) situado en la barra de estado
inferior de VS Code
5 Cargar el Firmware al Arduino:
* Con PlatformIO: Haz clic en la flecha hacia la derecha (→ Upload) en la barra inferior
6 Monitor Serie :
* Para observar las lecturas de distancia en tiempo real, abre el Monitor Serie haciendo clic en el icono del enchufe
