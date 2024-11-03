# Proyecto Electrónica Digital I - Tamagotchi👾

## Contenido
- [Proyecto Electrónica Digital I - Tamagotchi👾](#proyecto-electrónica-digital-i---tamagotchi)
  - [Contenido](#contenido)
  - [Integrantes](#integrantes)
  - [Diseño de Interfaz y Transiciones ✏️](#diseño-de-interfaz-y-transiciones-️)
  - [Especificaciones](#especificaciones)
    - [a. Sistema de botones](#a-sistema-de-botones)
    - [b. Sistema de sensado](#b-sistema-de-sensado)
    - [c. Sistema de visualización](#c-sistema-de-visualización)
    - [d. Manejo de necesidades e indicadores](#d--manejo-de-necesidades-e-indicadores)
  - [Descripción de Hardware](#descripción-de-hardware)
  - [Diagramas de flujo](#diagramas-de-flujo)
  - [Máquina de estados finitos](#máquina-de-estados-finitos)
  - [Diagrama del sistema](#diagrama-del-sistema)
  - [Simulaciones](#simulaciones)
  - [Analizador lógico](#analizador-lógico)
****
## Integrantes

- Andres Santiago Cañon Porras
- Mateo Bustos Aguilar
- Cristian Fabián Martínez Bohórquez

## Diseño de Interfaz y Transiciones ✏️

El diseño de la interfaz de nuestro Tamagotchi está centrado en brindar una interacción fluida y clara para el usuario. Para esto, se han definido los diferentes estados del Tamagotchi, las transiciones entre ellos y cómo se representarán visualmente. A continuación se describen los elementos principales:

- **Pantalla Principal**:

En esta pantalla se muestra el estado general de la mascota virtual, tales como el estado de ánimo, hambre, sueño, cura y vida de nuestra mascota.

<p align="center">
  <img src=https://github.com/user-attachments/assets/d1d8d0df-3d96-45fb-be85-b7963a24cf73>
</p>

Por otra parte, se diseñaron distintas animaciones de la mascota que describen la acción que está realizando en el momento (dormir, curar, comer, jugar), esto con el objetivo de que sea claro para el usuario que actividad está ejecutando la mascota.

<p align="center">
  <img src=https://github.com/user-attachments/assets/fad87c38-b790-432d-9429-f0f37beb3559>
</p>

- **Transiciones de Estado**:
  
  - Los estados principales que gestionan el comportamiento de la mascota son:
    
    - **Felicidad**: refleja cuán contenta está la mascota. Disminuye si no se juega con ella.
    - **Hambre**: indica cuán hambrienta está la mascota. Aumenta si no es alimentada.
    - **Sueño**: muestra el nivel de cansancio. Aumenta con el tiempo y se reduce cuando la mascota descansa.
    - **Cura (enfermedad)**: se activa cuando la mascota ha sido descuidada, indicando que está enferma y necesita atención médica.

- **Interfaz de Usuario**:

La interfaz se implementó mediante un soporte impreso en 3D, una pantalla OLED de 0,91 pulgadas (128 x 32 pixeles), una serie de botones físicos que permiten al usuario interactuar con la mascota, reiniciar el juego, cancelar alguna acción o ejecutar el *test*, así como un joystick que permite desplazarse por los distintos indicadores para que la mascota realice la respectiva acción.
  
<p align="center">
  <img src="https://github.com/user-attachments/assets/4789069b-5219-4b77-96df-a0ebcad8e81c">
</p>

- **Pantallas Secundarias**:
  
  Así mismo, se diseñaron ambientes para cada acción que esté ejecutando la mascota, esto con el fin de que la interacción usuario-mascota se sienta más amigable:
  
  - *Jugar*:
    
    ![jugar](https://github.com/user-attachments/assets/d84804cd-8418-4474-b0eb-433c0f1dba5e)
    
  - *Comer*:
    
    ![comer](https://github.com/user-attachments/assets/56670c4b-b048-47e9-9302-db2868d4f294)

  - *Dormir*:
    
    ![dormir](https://github.com/user-attachments/assets/e3552f65-322e-4d32-902d-74ac77d30048)
  
  - *Curar*:

    ![curar](https://github.com/user-attachments/assets/6645d3d7-13d1-42b5-ba7b-ddf4793689f8)
    
- Por otra parte, se diseñaron pantallas de inicio y de muerte:
  
  - *Inicio*:
    
    ![inicio](https://github.com/user-attachments/assets/d67b9ab3-c57f-4d45-af5e-4eebab1c18dd)

  - *Muerte*:

    ![muerte](https://github.com/user-attachments/assets/690b99cc-a86b-4352-b148-fd9144adbb24)

## Especificaciones

La FPGA está programada para simular distintos estados de la mascota, basándose en el comportamiento y la interacción con el usuario a través de al menos tres sistemas principales:

### a. Sistema de botones

<p align="center">
  <img src="https://github.com/user-attachments/assets/1831e325-d094-49d5-a2fb-e53f3b6f33d7">
</p>
  
  La interacción usuario-sistema se realizará mediante los siguientes botones configurados:
  
  - **Reset**: Reestablece el Tamagotchi a un estado inicial conocido al mantener pulsado el botón durante al menos 5 segundos. Este estado inicial simula el despertar de la mascota con salud óptima.

  - **Cancel**: Permite al usuario salir de las opciones y modos de interacción, retornándolo al menu principal.
  
  - **Test**: Activa el modo de prueba al mantenerlo pulsado por al menos 5 segundos, permitiendo al usuario navegar entre los diferentes estados del Tamagotchi con cada pulsación.

  - **Select (Joystick)**: Permite al usuario desplazarse por los diferentes indicadores del modo de interacción.

  - **Action (Joystick)**: Permite al usuario luego de desplazarse por los indicadores decidir cual de las acciones realizar o repetir.

  

### b. Sistema de Sensores

Para integrar al Tamagotchi con el entorno real y enriquecer la experiencia de interacción, se incorporará al menos un sensor que modifique el comportamiento de la mascota virtual en respuesta a estímulos externos. Los sensores permitirán simular condiciones ambientales y actividades que afecten directamente el bienestar de la mascota.

- **Conversor de Voltaje (Joystick)**: El conversor de voltaje se utiliza para asegurar que la señal esté dentro de un rango adecuado, permitiendo su correcta interpretación y detección del movimiento.

- **Sensor Ultrasonido**: Permitirá al usuario luego de seleccionar la interacción dormir, despertar a la mascota si el usuario se acerca a el sensor.

### c. Sistema de visualización

Para visualizar todas las interacciones y estados del dispositivo se utilizara únicamente un módulo display LCD OLED SPI

- Voltaje de Operación DC: 3V ~ 5V
- Controlador: SSD1306
- Resolución: 128 x 32

  <p align="center">
    <img src=https://github.com/user-attachments/assets/70f14481-869c-4089-9578-7f43465e5de7>
  </p>

### d. Manejo de necesidades e indicadores

Se tendra una serie de atributos los cuales estaran asociados a diferentes valores, y según dichos valores y algún limite establecido se definirán las necesidades de la mascota.

<div align="center">

| ***Atributos*** | ***Valores*** |
| :-----------: | :---------: |
|    Hambre     |   0 - 100   |
|     Sueño     |   0 - 100   |
|   Diversión   |   0 - 100   |
|     Vida      |   0 - 100   |

</div>

<p align="center">
    <img src=https://github.com/user-attachments/assets/7b86d0e1-7cbc-4aae-8779-bf5c758d76e9>
</p>

## Descripción de Hardware

<div align="center">

| ***Nombre***        |  ***Referencia***                             |   ***Imagen***                                                                                   |***Descripción*** |  ***Datasheet*** |
| :-----------:       | :---------:                                   | :---------:                                                                                      | :---------:      | :---------:      |
| Pantalla OLED       |   OLED Display 0.91"                          |   ![oled (2)](https://github.com/user-attachments/assets/50b60b46-4207-4c44-9626-d0c27bb06b46)   |   <br>La pantalla OLED de 0.91" es un display compacto de tipo OLED (Diodo Orgánico Emisor de Luz), tiene un tamaño de 0.91 pulgadas, generalmente con una resolución de 128x32 píxeles, y se caracteriza por su alto contraste, brillo, y amplio ángulo de visión.<br> |  [Link](http://www.lcdwiki.com/res/MC091GX/SSD1306-Revision%201.5.pdf)        |
|     FPGA            |   ALTERA Cyclone IV EP4CE6E22C8N              |   ![FPGA (1)](https://github.com/user-attachments/assets/b95f1e59-8a16-4553-98f7-a312b09973e3)   |  <br> Es un dispositivo programable de lógica avanzada (FPGA) de la familia Cyclone IV, desarrollada por Altera (ahora parte de Intel). Esta FPGA está diseñada para aplicaciones de bajo costo y bajo consumo de energía, ideal para proyectos de electrónica digital y sistemas embebidos. <br>        |   [Link](https://www.mouser.com/datasheet/2/612/cyiv_51001-1299459.pdf)        |
|  Sensor Ultrasonido |  HCSR04                                       |   ![A1 (1)](https://github.com/user-attachments/assets/02ab6477-c7b0-459d-a84b-a35ad791daf9)     |   <br> El sensor ultrasónico HC-SR04 es un dispositivo ampliamente utilizado para medir distancias a través de ondas de ultrasonido. Funciona emitiendo un pulso ultrasónico y midiendo el tiempo que tarda en regresar tras reflejarse en un objeto. Este tiempo se convierte en una medida de distancia, generalmente en centímetros. <br>        |   [Link](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)        |
|     Joystick        |   DUAL XY ANALOGO CON PULSADOR                |   ![3-17 (1)](https://github.com/user-attachments/assets/63f6a59f-dd0d-45a1-9dee-e4200c51cf87)   |   <br> Es un joystick analógico que detecta movimientos en dos ejes (X e Y) y cuenta con un botón integrado (pulsador). Los ejes X e Y corresponden al movimiento horizontal y vertical, respectivamente, y cada uno genera una señal analógica que varía según la inclinación del joystick. <br>       |   [Link](https://naylampmechatronics.com/img/cms/Datasheets/000036%20-%20datasheet%20KY-023-Joy-IT.pdf)        |

</div>

## Diagramas de flujo

- **_General_**:

Este diagrama muestra cómo el sistema responde a las variaciones en las necesidades del Tamagotchi a lo largo del tiempo y cómo permite al usuario interactuar con él. A medida que el tiempo avanza, se activan diferentes estados como hambre, sueño o fatiga, representados en los bloques centrales del flujo. El usuario puede elegir entre acciones como jugar, alimentar, curar o dejar que descanse, lo que influye directamente en los valores de las variables life, disease y death. Estas variables cambian en función de cómo se atienden las necesidades del Tamagotchi.

El diagrama también destaca que, si no se gestionan adecuadamente las necesidades, la variable disease podría activarse, lo que podría llevar al estado de death si no se toman medidas a tiempo. Además, se incluyen rutas alternativas como reset, que reinicia el ciclo, y la opción de realizar un test, un mecanismo que permite verificar ciertos estados del Tamagotchi antes de continuar.

  <p align="center">
    <img src=https://github.com/user-attachments/assets/cc9e54d6-5540-4a3a-ab70-5e8e26670b56>
  </p>

- **_Necesidades_**:

El diagrama de flujo siguiente muestra el ciclo de vida de nuestra mascota que tiene atributos de vida, comida, diversión y descanso. Cada 0.8 segundos, estos valores disminuyen, lo que afecta el estado de vida. Si la vida llega a 0, se activa la muerte. Si la vida es menor que 16, se activa la variable disease, que influye directamente en la vida de la mascota.


  <p align="center">
    <img src=https://github.com/user-attachments/assets/2aaac5ae-2807-4d9c-bbcc-0b18ad60a5a6>
  </p>

- **_Casos de interacción_**:

Los siguientes diagramas representan los casos de interacción a los que el usuario puede acceder dependiendo el menú/estado que se seleccione, es de suma importancia tener presente como funciona cada uno de estos menús para conocer el funcionamiento del tamagotchi y estar al tanto de como suben y bajan los indicadores conforme el tiempo avanza.

![diagrama necesidades1 drawio](https://github.com/user-attachments/assets/6b863574-c685-40da-a53f-f07a1133f6a3)


## Máquina de estados finitos

<p align="center">
  <img src=https://github.com/user-attachments/assets/3f63bbfb-6ce2-4bee-94b3-160a88e32143>
</p>

- Modo test

<p align="center">
  <img src=https://github.com/user-attachments/assets/2051398f-ba6d-4f86-a562-6030697d5557>
</p>

## Diagrama del sistema

<p align="center">
    <img src=https://github.com/user-attachments/assets/cc9e54d6-5540-4a3a-ab70-5e8e26670b56>
</p>

## Simulaciones

- **_ssd1306_master_**

I2C-bus Write data:

<p align="center">
  <img src=https://github.com/user-attachments/assets/e21a4aa7-6525-4379-8b15-c063cef69f97>
</p>

Gtkwave:

<p align="center">
  <img src=https://github.com/user-attachments/assets/665b2729-0e32-46bf-84dd-f93b46437e35>
</p>

En el diagrama del datasheet, se describe cómo se envía una secuencia de bytes, comenzando por la dirección del esclavo, seguida de un byte de control y posteriormente varios bytes de datos o comandos. Este proceso es exactamente lo que se observa en la simulación: la comunicación I2C se inicia con el envío de la dirección del esclavo, luego se transmite el byte de control, y finalmente, los datos o comandos necesarios para la configuración de la pantalla.

En la simulación, también se pueden ver claramente las señales de reconocimiento (ACK) que ocurren después de cada byte transmitido, confirmando que el esclavo está recibiendo los datos como lo dicta el protocolo I2C. Esto asegura que cada paso del proceso de comunicación, desde la dirección hasta los datos, está siendo aceptado correctamente por el dispositivo esclavo.

Además, la simulación refleja cómo la comunicación pasa por diferentes estados del protocolo. Estos estados coinciden con los que describe el datasheet para la transmisión de bytes, gestionando cada fase de la comunicación I2C. Desde la dirección del esclavo hasta la escritura de comandos o datos, la simulación sigue el flujo de manera precisa, mostrando un ciclo completo de escritura en la pantalla OLED, tal como lo detalla el datasheet del SSD1306.

- **_ads1115_master_**

Two-Wire Timing Diagram for Read Word Format

<p align="center">
  <img src=https://github.com/user-attachments/assets/8ae2c961-3bf6-4f1a-a26e-9a292503c055>
</p>

Two-Wire Timing Diagram for Write Word Format:

<p align="center">
  <img src=https://github.com/user-attachments/assets/d5b27520-49f2-437e-88b5-1ff434722237>
</p>

Gtkwave:

<p align="center">
  <img src=https://github.com/user-attachments/assets/439314e4-0a78-4442-b77c-c30e80e179a2>
</p>

En el diagrama del datasheet del ADS1115, se describe cómo se realiza el proceso de comunicación I2C, comenzando por el envío de la dirección del esclavo, seguida de la selección de un registro y posteriormente los datos de configuración o conversión. Este proceso es replicado fielmente en la simulación: la secuencia inicia con la transmisión de la dirección del ADS1115, seguida del byte que indica el registro que se va a configurar, y luego se envían los bytes de configuración necesarios para establecer parámetros como la ganancia y la velocidad de muestreo del ADC.

Durante la simulación, se observa claramente cómo se generan las señales de reconocimiento (ACK) tras la transmisión de cada byte, lo que confirma que el dispositivo ADS1115 está recibiendo correctamente los datos, como lo dicta el protocolo I2C. Esta validación es crucial para asegurar que cada paso, desde la dirección hasta los datos de configuración, se está llevando a cabo sin errores.

La simulación también refleja la transición a los diferentes estados del protocolo I2C, tal como se describe en el datasheet. Aunque el proceso de selección del registro de conversión y la lectura de los dos bytes correspondientes al valor convertido fue programado, debido a la complejidad de replicar el comportamiento exacto del convertidor ADC, esta parte no se ilustra completamente en la simulación.

- **_top_hcsr04_**

Gtkwave:

<p align="center">
  <img src=https://github.com/user-attachments/assets/17ee4299-b1ab-4849-bed9-4ab149788957>
</p>

En el diagrama del datasheet del HCSR04, se describe cómo el sensor emite un pulso de "trigger" para iniciar la medición de distancia, seguido por la espera de un pulso de "echo" que indica la recepción de la señal reflejada. Este proceso fue replicado en la simulación: tras enviar el pulso de trigger, el sistema empieza a contar el tiempo hasta que se recibe el pulso de echo, lo que permite calcular la distancia en función del tiempo transcurrido.

En la simulación, se observa cómo el contador comienza justo después del trigger y continúa hasta que el pulso de echo es recibido. La distancia calculada, una vez determinada, se clasifica en dos niveles: nivel1 y nivel2, que corresponden a diferentes rangos de distancia según qué tan lejos esté el objeto detectado. Aunque la simulación no ilustra el cálculo exacto de la distancia, se enfoca en mostrar el proceso de emisión del trigger y la recepción del echo, y cómo los niveles resultantes se asignan de acuerdo con la distancia medida.

## Analizador lógico

- **_Pantalla oled_**

<p align="center">
  <img src=https://github.com/user-attachments/assets/22058cd4-fc61-4a19-8c4a-3677f1a79c24>
</p>

En la evaluación del funcionamiento del código para la pantalla OLED 128x32 (SSD1306), se utilizó un analizador lógico para capturar y analizar las señales en el bus I2C. Los resultados confirmaron que la pantalla estaba operando correctamente. El analizador mostró la secuencia adecuada de la dirección del esclavo, seguida de los bytes de control y los datos necesarios para inicializar la pantalla y dibujar gráficos. Las señales de reconocimiento (ACK) generadas después de cada byte transmitido indicaron que el OLED estaba recibiendo los datos sin errores, validando así la correcta implementación del protocolo I2C en el código.

- **_Conversor A/D (Joystick)_**

<p align="center">
  <img src=https://github.com/user-attachments/assets/fa526531-874a-4bdf-84da-58099ecc2e05>
</p>

En la evaluación del código para el conversor A/D (ADS1115), el analizador lógico se utilizó para registrar y analizar las señales en el bus I2C durante el proceso de configuración y lectura. Los resultados mostraron que el ADS1115 estaba respondiendo adecuadamente a las instrucciones enviadas. Se observaron las transiciones correctas en el bus I2C al seleccionar el registro de configuración y al leer el valor digitalizado, lo que confirma que el dispositivo estaba operando según lo esperado. Además, se registró la emisión del pulso de trigger y la recepción de los datos de conversión, indicando que el ADC estaba funcionando de manera efectiva.

## Video prueba

<p align="center">
  <video src="https://github.com/user-attachments/assets/cbe0fcec-eda6-44f3-8e6a-52cdbb66d697">
<p/>
