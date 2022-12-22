# Arducky

Es una herramienta de inyección de teclas disfrazada como una unidad flash genérica. Las computadoras lo reconocen como un teclado normal y aceptan cargas útiles de teclado preprogramadas a más de 1000 palabras por minuto.
Las cargas útiles se elaboran con un lenguaje de scripting simple y se pueden usar para colocar shells invertidos, inyectar binarios, códigos pin de fuerza bruta y muchas otras funciones automatizadas para el probador de penetración y el administrador de sistemas.
Arducky es una manera de llamar a un Arduino haciendo de Rubber Ducky.

## ¿Por qué?

Basicamente porque no podia comprar el Rubber Ducky, así que busqué proyectos en interner y me puse a ~~experimentar~~ jugar.
Tambien la licencia [OSHW](https://www.oshwa.org/definition/spanish/) y [GNU GENERAL PUBLIC LICENSE V3](https://www.gnu.org/licenses/gpl-3.0.txt) son más que suficiente para poder tener total livertad para poder crear.

## Hardware

- [Arduino Pro Micro](http://dlnmh9ip6v2uc.cloudfront.net/datasheets/Dev/Arduino/Boards/ATMega32U4.pdf) (Leonardo) con un micro controlador ATmega32u4 (32KB flash y 2.5KB ram) con Bootloader
- [Modulo Micro SD](https://cdn-learn.adafruit.com/downloads/pdf/adafruit-micro-sd-breakout-board-card-tutorial.pdf): nos permite insertar una memoria Micro SD que son las más comunes en el mercado, el modulo se puede alimentar con 3.3V o 5V usando los pines  respectivos. 
- Una tarjeta Micro SD. 

> **NOTA:** Vemos que el microcontrolador ATmega32u4 se puede encontrar en otras placas como el arduino uno o el arduino mini. 

### Como conectar los pines

![Pro_micro](https://user-images.githubusercontent.com/120866208/209189332-74987010-af15-45d6-921a-ea017662d1e7.png)

> **NOTA:** Es recomendable que usemos los cables para protoboard así nos aseguramos las conexiones. Acá les dejo un [videos](https://www.youtube.com/watch?v=ksvo1WDYQ7s) de las conexiones y como usarlo.

## Software

### Instalamos la libreria del teclado

Debemos comprobar que la version por defecto que tiene el IDE de la libreria keyboard sea la 1.0.1, de lo contrario, puede saltar un error.
Se debe instalar esta versión personalizada de la biblioteca del teclado Arduino. Para eso debemos [descargar](https://github.com/ernesto-xload/arduino_keyboardlib) el archivo y abrir el IDE de Arduino.
Una vez abierto lo instalamos.

### Instalar el código

* Descargamos el archivo
* Descomprime el archivo descargado cuando quieras trabajar.
* Abrir Arduino IDE
* Abrir el archivo ducky_interpreter.ino
* Seleccione la placa Arduino Leonardo
* Conecte la placa a su computadora
* Incluimos la libreria keyboard.h
* Dejamos solamente los #include y agregamos el #define correspondiente
* Por ejemplo: #include<keyboard.h> y #define kbd_es_es

### Comandos

* **ALT** [key name] (ex: ALT F4, ALT SPACE)
* **CTRL** [key name] (ex: CTRL ESC)
* **DELAY** [Time in millisecond * 10] (used to overide temporary the default delay)
* **COMMAND** (For OSX Users ex: COMMAND SPACE)
* **GUI** or **WINDOWS** [key name] (ex: GUI r, GUI l)
* **REM** [anything] (used to comment your code, no obligation)
* **SHIFT** [key name] (ex: SHIFT DEL)
* **STRING** [any character of your layout]
* **REPEAT** [Number] (Repeat last command N times)
* **TAB** not just a cola
* **DOWNARROW** | **DOWN**
* **LEFTARROW** | **LEFT**
* **RIGHTARROW** | **RIGHT**
* **UPARROW** | **UP**
* **PRINTSCREEN** Typically takes screenshots
* **MENU** or **APP** Emulates the App key
* **ESC** or **ESCAPE** You can never
* **HOME** There's no place like
* **INSERT**
* **SPACE** the final frontier
* **DELETE**
* **PAGEUP**
* **PAGEDOWN**
* **BREAK** or **PAUSE** For the infamous combo CTRL BREAK
* **END** When will it ever

### Crear tus payload's

Como se vé en la imagen no escomplicado para nada, solamente con el DELAY esperamos 3 segundos para que el comprolador sea tomado por windows, luego con el comando GUI r (es la tecla windows + r) lanzamos la ventana ejecutar y escribimos calc con el comando STRING y lo corremos con el enter.

```shell
REM Mostramos un archivo txt en pantalla que dice 'Hello World!!!'
DELAY 3000
GUI r
DELAY 500
STRING notepad
DELAY 500
ENTER
DELAY 750
STRING Hello World!!!
ENTER
```

### ¿Necesitamos compilar el código?

No es necesario, ya que el mismo software que se encuestra en el arduino se encarga de interpretar y ejecutar los comandos que le dimos en el script.txt

## Utilizar

* Guarda el payload que creaste con el nombre de script.txt
* Guárdalo en la tarjeta sd.
* Inserta tarjeta microsd en tu ArDucky.
* Los [payloads](https://github.com/hak5/usbrubberducky-payloads.git) de Rubber Ducky tambien funcionan.

## Ejemplo de uso

https://www.youtube.com/watch?v=prRtnkIW21M

Este es un ejemplo básico de como extraer PDF's (o cualquier archivo), de una maquina a una USB auxiliar, por si la pc que se quiere extraer los archivos no cuenta con conexión a internet Como funciona.

## Descargar

```shell
git clone https://github.com/aguztynbassi/Arducky.git
```
