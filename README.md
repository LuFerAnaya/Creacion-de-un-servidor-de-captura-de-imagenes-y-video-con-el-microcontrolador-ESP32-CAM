# Universidad Tecnológica de México.

**Procesamiento Digital de imágenes**

Nombre del Alumno:  

 **- Petriciolet Cortes Josue Michel, Matricula 20922674** 
 **- Santa Cruz Hernández Logan Diego, Matricula 20580787** 
 **- Tovar Barrera Israel, Matricula 21128157** 
 **- Vargas Anaya luisa Fernanda Matricula, 14899294**** 
 
 Ingeniería en sistemas computacionales 
 Grupo: EC08S 
 Profesor: M. En C. Raymundo Soto Soto 
 Práctica: #3 
 Título de la practica: Creación de un servidor de captura de imágenes y vídeo con el microcontrolador ESP32 CAM.
 Fecha de entrega: 12 / 11 / 2022

**Objetivos:** Programar un servidor webcam usando el controlador ESP32 CAM, el IDE de Arduino y Python para capturar y visualizar imágenes y vídeo. Introducción Como se ha visto en la primera parte del curso, el procesamiento de imágenes realiza muchas transformaciones de la información contenida de una imagen digital y esto se traduce en cambios que nos permiten visualizar, corregir, mejorar, cambiar o extraer los datos de intensidad de color en las dichas imágenes. Hemos visto también que el procesamiento de las imágenes se da en varias etapas y cada etapa es importante porque en cada una de ellas se mejorar la información que se está tratando. En Los sistemas de PDI (o sistemas de visión artificial) las etapas más importantes son la adquisición, el preprocesado, la segmentación, el reconocimiento y la descripción de la imagen. En esta práctica abordaremos la etapa de adquisición de imagen digitales programando un circuito que nos permita obtener imágenes digitales que se enviaran a un servidor web y a las que podremos acceder vía WiFi o vía streaming. Microcontrolador ESP32 CAM EL ESP32 CAM es un SoC (System On a Chip), fabricado por la empresa AI Thinker, es una tarjeta de desarrollo que integra una pequeña cámara OV2640 2MP que puede funcionar de manera independiente además de un módulo WiFi con Bluetooth. La cámara OV2640 de 2MP integra un sensor de imagen CMOS UXGA (1632x1232) de 1/4 de pulgada. El pequeño tamaño del sensor y el bajo voltaje de operación brindan todas las características de una sola cámara UXGA y un procesador de imágenes. A través del control de bus SCCB, puede generar datos de imagen de 8/10 bits de varias resoluciones, como fotograma completo, submuestreo, zoom y ventanas. La imagen UXGA de esta cámara puede alcanzar hasta 15 cuadros por segundo (hasta 30 cuadros para SVGA y 60 cuadros para CIF). Los usuarios tienen un control completo sobre la calidad de la imagen, el formato de datos y la transmisión. La plataforma ESP32 permite el desarrollo de aplicaciones en diferentes lenguajes de programación, frameworks, librerías y recursos diversos. Los más comunes a elegir son: Arduino (en lenguaje C++), Esp-idf (Espressif IoT Development Framework) desarrollado por el fabricante del chip, Simba Embedded Programming Platform (en lenguaje Python), RTOS's (como Zephyr Project, Mongoose OS, NuttX RTOS), MicroPython, LUA, Javascript (Espruino, Duktape, Mongoose JS), Basic. Al trabajar dentro del entorno Arduino podremos utilizar un lenguaje de programación conocido y hacer uso de un IDE sencillo de utilizar, además de hacer uso de toda la información sobre proyectos y librerías disponibles en internet. La comunidad de usuarios de Arduino es muy activa y da soporte a plataformas como el ESP32 y ESP8266. Dentro de las principales placas de desarrollo o módulos basados en el ESP32 tenemos: ESP32-WROOM-32, NodeMCU-32 ESP32 y ESP32-CAM y de la familia ESP8266 tenemos: ESP-01, ESP-12E, Wemos D1 mini y NodeMCU v2. Todo lo anterior permite usar el controlador en una gran cantidad de sistemas embebidos que requieran el procesamiento de imágenes. Especificaciones técnicas del ESP32 CAM  Voltaje de alimentación: 5VDC  Voltaje entradas/salidas (GPIO): 3.3VDC  SoM: ESP-32S (Ai-Thinker)  SoC: ESP32 (ESP32-D0WDQ6)  CPU: Dual core Tensilica Xtensa LX6 (32 bit)  Frecuencia principal de hasta 240 MHz  Potencia informática de hasta 600 DMIPS  Velocidad de reloj de hasta 160 MHz  Wifi 802.11b/g/n, Bluetooth 4.2  Antena PCB, también disponible conexión a antena externa  520KB SRAM interna, 4MB SRAM externa  Soporta UART/SPI/I2C/PWM/ADC/DAC  Incluye socket para TF card micro-SD  Cámara OV2640  Resolución fotos: 1600 x 1200 pixels  Resolución vídeo: 1080p30, 720p60 y 640x480p90  Incluye LED de flash en placa  Óptica de 1/4"  Dimensiones: 27_40.5_6 mm  Peso: 20 gramos  Para mayor cantidad de información revisar el datasheet de la tarjeta en este vínculo

Lenguajes en los que se puede programar el ESP32 CAM  Arduino IDE (en lenguaje C++),  Esp-idf (Espressif IoT Development Framework) desarrollado por el fabricante del chip,  Simba Embedded Programming Platform (en lenguaje Python)  MicroPython  Javascript (Espruino, Duktape, Mongoose JS)  Atom  Etc. El esp32 es una placa de bajo costo y grandes capacidades, integra CPU, memoria RAM volátil y no volátil (Para el programa) y varios dispositivos de I/O (Entrada y salida) en un chip único, además de dispositivos de comunicaciones variados, que podemos emplear para recibir y enviar información al exterior. Básicamente el ESP32 es capaz de recibir señales digitales (Digital Inputs), enviar señales digitales (Digital Output), recibir señales analógicas en tensión (Analog Input) mediante ADCs, enviar señales analógicas al exterior (Analog Output) como señales moduladas en pulsos PWM y con 2 convertidores digital a analógico (DAC) detectar variaciones de capacidad en los pines adecuados, además de comunicarse con el exterior de forma cableada con Buses I2C integrados, buses SPI integrados y puertos UART o serie programables. También puede comunicarse con el exterior de forma inalámbrica: puerto WiFi integrado con stack TCPIP y puerto Bluetooth 5. En esta práctica usaremos la mayor cantidad de capacidades para obtener imágenes digitales. Imágenes del microcontrolador ESP32 CAM

[![image](https://user-images.githubusercontent.com/108105124/201498879-2e593046-0c37-4815-8c72-e82fba907d92.png)](https://user-images.githubusercontent.com/108105124/201498879-2e593046-0c37-4815-8c72-e82fba907d92.png)

Imagen 1. Vista posterior y anterior del microcontrolador ESP32 Cam con cámara OV2640 de 2 MP. En la imagen de abaja se muestra un ESP32 CAM conectado a un circuito convertidor usb-ttl para programarlo y alimentar la corriente de 5 V. El cable utilizado es USB a mini-usb.

[![image](https://user-images.githubusercontent.com/108105124/201498881-1cafe040-5b30-4289-80d5-37ab952fad41.png)](https://user-images.githubusercontent.com/108105124/201498881-1cafe040-5b30-4289-80d5-37ab952fad41.png)

Imagen 2. Detalle del circuito convertidor usb-ttl, esta placa permite la comunicación serial entre la computadora el ESP32 CAM. Material Necesario  Microcontrolador ESP32 CAM con cámara OV2640  Circuito convertidor USB-TTL  Cable de datos USB-USB mini  Cable de red  Computadora  Modem (se conectará el esp32 con SSID y el password del modem)

Software necesario El software se instalará en la computadora donde conectaremos nuestro ESP32 CAM. Respetar la versión del software que se indica para evitar conflictos entre las bibliotecas.  
• IDE de Arduino 1.8.19 • Drivers (Windows) para el esp32 cam (se comparte en el material semanal) • IDE de Python (se recomienda la versión 3.7 de Python) o La biblioteca OpenCv para python versión 4.2.x • Bibliotecas de Arduino para el manejo del esp32 CAM o  [https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json](https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json)  (en preferencias-- Gestor de URLS) o Instalar en el la tarjeta ESP32 de Expressif Systemas o La biblioteca CameraWebServer de los ejemplos para la ESP32 CAM de AI Thinker • Navegador web  
Desarrollo. Para poder visualizar las imágenes y vídeo capturadas con la cámara del ESP32 CAM es necesario crear un servidor web, el procedimiento descrito a continuación nos permitirá crear el servidor web para visualizar en un navegador y en Python las imágenes y vídeo.

1.  Descargar e Instalar el IDE de Arduino 1.18.19 de la página oficial  [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)

[![image](https://user-images.githubusercontent.com/108105124/201498899-4761cd78-6f9c-4d46-8f13-c9e9b2daf2d2.png)](https://user-images.githubusercontent.com/108105124/201498899-4761cd78-6f9c-4d46-8f13-c9e9b2daf2d2.png)

2.  Instalar los drivers para establecer la conexión serial entre el circuito de la ESP32 CAM y la computadora. Los drivers son los CH34x para Windows. Si se instala en Linux no es necesario instalarlos ya que vienen por default.
3.  Dar de alta la tarjeta ESP32 cam en el IDE de Arduino en el menú archivo >> preferencias y el campo de gestor de URLS adicionales escribir  [https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json](https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json)

[![image](https://user-images.githubusercontent.com/108105124/201499383-fc431870-cb8a-451f-b83e-2a5f365828a7.png)](https://user-images.githubusercontent.com/108105124/201499383-fc431870-cb8a-451f-b83e-2a5f365828a7.png)

4.  En el IDE de Arduino ir a Herramientas>> Placa >> Gestor de tarjetas, buscar la placa ESP32 CAM de Expressiff Systems e instalarla. En caso de que no aparezca la placa revisar el paso anterior.

[![image](https://user-images.githubusercontent.com/108105124/201499387-9e1af3e4-928c-4eb6-8e79-188ac6d0ca04.png)](https://user-images.githubusercontent.com/108105124/201499387-9e1af3e4-928c-4eb6-8e79-188ac6d0ca04.png)

[![image](https://user-images.githubusercontent.com/108105124/201499388-5bfe311f-33f3-49d9-aa57-be37e9764f90.png)](https://user-images.githubusercontent.com/108105124/201499388-5bfe311f-33f3-49d9-aa57-be37e9764f90.png)

5.  Después de instalar la tarjeta hay que elegir la placa ESP32 de AI Thinker para poder programarla, se elige en el menú herramientas >> placa >> ESP32 arduino >> AI Thinker ESP32-CAM. Al finalizar hay que conectar la placa al puerto USB.

[![image](https://user-images.githubusercontent.com/108105124/201499392-79fa8f28-ef26-453c-b4fc-dfa71cb9d5af.png)](https://user-images.githubusercontent.com/108105124/201499392-79fa8f28-ef26-453c-b4fc-dfa71cb9d5af.png)

6.  Una vez configurada la placa se debe revisar que haya comunicación serial entre el dispositivo y la computadora, por lo que hay que tener conectada el ESP32 a la computadora, para esto hay que ir al menú herramientas >> monitor serie. Otra forma de saber si hay comunicación es revisar si hay puerto disponible en el menú >> puerto, si aparece un puerto habilitado es indicio de que hay comunicación. Al momento de revisar la comunicación con la primera opción hay que colocar la velocidad del monitor serial en 9600 o 115600 baudios para obtener texto que indique la comunicación. Dado que estamos usando la placa ESP32 con el convertidor usb-ttl sólo es necesario oprimir el botón de download o reset para saber si está comunicándose con la computadora.

[![image](https://user-images.githubusercontent.com/108105124/201499396-7f785141-df0f-4679-809a-42f02b6d87f1.png)](https://user-images.githubusercontent.com/108105124/201499396-7f785141-df0f-4679-809a-42f02b6d87f1.png)

7.  Establecida la comunicación serial entre el ESP32 y la computadora procedemos a cargarle el programa que nos permite crear el servidor web para tomar imágenes y vídeo, para esto abriremos el programa que se encuentra en Archivo >> Ejemplos >> ESP32 >> Camera >> CameraWebServer

[![image](https://user-images.githubusercontent.com/108105124/201499407-b9d6f42e-42ce-4c05-8596-23af4b75910b.png)](https://user-images.githubusercontent.com/108105124/201499407-b9d6f42e-42ce-4c05-8596-23af4b75910b.png)

El programa aparecerá cargado en el editor de código de Arduino, antes de cargarlo hay que configurarlo.

8.  Antes de cargar el código a la tarjeta debemos definir el tipo de cámara que estamos usando (en nuestro caso es CAMERA_MODEL_AI_THINKER) y colocar el nombre de la red wifi a la que nos conectaremos con el ESP32 CAM (aquí prendemos el modem y conectamos la computadora al mismo con el cable de red) y el password de la red.

[![image](https://user-images.githubusercontent.com/108105124/201499411-1c940a62-d6ec-44be-8a44-d0f28800532b.png)](https://user-images.githubusercontent.com/108105124/201499411-1c940a62-d6ec-44be-8a44-d0f28800532b.png)

9.  Realizado lo anterior nos cercioramos que este conectado el ESP32 al puerto USB. Abrimos el monitor serial para revisar el status de la compilación y subida del código, oprimimos el botón de reset del ESP32 CAM una vez y subimos el código a la placa usando el botón subir. Esto comenzará a programar el ESP32, tardará unos segundos

[![image](https://user-images.githubusercontent.com/108105124/201499415-3a01eb6a-ea52-40a0-ab35-ee627ad79d17.png)](https://user-images.githubusercontent.com/108105124/201499415-3a01eb6a-ea52-40a0-ab35-ee627ad79d17.png)

10.  Al finalizar la programación del ESP32 en el monitor serial debemos ver un mensaje como el siguiente

[![image](https://user-images.githubusercontent.com/108105124/201499419-baa3320b-a0c8-426f-bae3-978f79cdfa4e.png)](https://user-images.githubusercontent.com/108105124/201499419-baa3320b-a0c8-426f-bae3-978f79cdfa4e.png)

Del mensaje anterior nos interesa la última línea que nos informa la dirección IP donde podemos visualizar las imágenes de la cámara web del ESP32 CAM Camera Ready! Use ‘[http://192.168.x.xx’](http://192.168.x.xn--xx-o2t/)  to connect Copiamos y pegamos la dirección en un navegador web y ya tendremos listo nuestro servidor para recibir imágenes y vídeo del microcontrolador ESP32 CAM. En el navegador se deberá ver algo parecido a esto, una pagina con los controles para iniciar streaming de vídeo o captura de imágenes. Para comenzar el streaming pulsa el botón de start streaming.

[![image](https://user-images.githubusercontent.com/108105124/201499425-34588b0a-91e0-4b29-9907-f81ca66d877e.png)](https://user-images.githubusercontent.com/108105124/201499425-34588b0a-91e0-4b29-9907-f81ca66d877e.png)

10.  Una de las características del servidor es que podemos exportar las imágenes para realizar alguna otra aplicación. En esta parte realizaremos un ejemplo de cómo hacer la exportación de imágenes a Python y OpenCv desde el servidor. • Anaconda Navigator  [https://www.anaconda.com/](https://www.anaconda.com/)  • Al finalizar la instalación de Anaconda instalamos, usando el prompt de Anaconda ejecutado como administrador, la versión 4.4.0.46 de OpenCv usando el comando pip install opencv-contrib-python==4.4.0.46

[![image](https://user-images.githubusercontent.com/108105124/201499426-bcb55ae2-6a63-465e-ab74-c78a29096752.png)](https://user-images.githubusercontent.com/108105124/201499426-bcb55ae2-6a63-465e-ab74-c78a29096752.png)

• Abrimos el editor de código de Spyder y pegamos el siguiente código

import cv2 from urllib.request import urlopen import numpy as np

stream = urlopen('[http://192.168.xx.x:81/stream](http://192.168.xx.x:81/stream)') # En esta línea pegar la dirección bytes = bytes() while True: bytes += stream.read(1024) a = bytes.find(b'\xff\xd8') b = bytes.find(b'\xff\xd9') if a != -1 and b != -1: jpg = bytes[a:b+2] bytes = bytes[b+2:] if jpg : img = cv2.imdecode(np.fromstring(jpg, dtype=np.uint8), cv2.IMREAD_COLOR) cv2.imshow('ESP32 CAM', img) if cv2.waitKey(1) & 0xff == ord('q'): break stream.release() cv2.destroyAllWindows()

En la línea correspondiente a la variable stream pegamos la dirección que nos arrojó el monitor serial para visualizar las imágenes del ESP32 CAM. Con lo anterior ya estamos usando imágenes obtenidas de nuestro microcontrolador.

**Resultados:**

Lo primero que podemos ver en la aplicación de la cámara por servidor es la calidad donde podemos ajustar el tamaño de los pixeles entre más grandes los pixeles peor se ve la imagen y entre más pequeños mejor se ve.

[![image](https://user-images.githubusercontent.com/108105124/201499437-930b4507-117a-4a88-8f5d-09ea8830aa4d.png)](https://user-images.githubusercontent.com/108105124/201499437-930b4507-117a-4a88-8f5d-09ea8830aa4d.png)

En esta otra opción podemos ajustar el brillo de la camara como vimos dependiendo de la luz en la imagen podemos aumentarla o reducirla para que se vea más información o menos dependiendo cual sea el caso

[![image](https://user-images.githubusercontent.com/108105124/201499442-fed74c94-b11c-4cc5-9699-53707e2cbb23.png)](https://user-images.githubusercontent.com/108105124/201499442-fed74c94-b11c-4cc5-9699-53707e2cbb23.png)

En este apartado podemos ajustar el contraste de la imagen dependiendo nuestras necesidades de la imagen con el que podemos trabajar y mostrar la información que necesitemos.

[![image](https://user-images.githubusercontent.com/108105124/201499446-e99edd2b-9826-4ad3-abd7-f84162ffcbc2.png)](https://user-images.githubusercontent.com/108105124/201499446-e99edd2b-9826-4ad3-abd7-f84162ffcbc2.png)

Aquí podemos ver la saturación que necesitemos en la imagen y la podemos ajustar lo que necesitemos en la imagen tanto negativos como positivos.

[![image](https://user-images.githubusercontent.com/108105124/201499449-3b4a1bca-837d-45b9-9e40-9f933a74e1f4.png)](https://user-images.githubusercontent.com/108105124/201499449-3b4a1bca-837d-45b9-9e40-9f933a74e1f4.png)

En la aplicación existe la opción de poner la imagen en negativo como podemos observar y existen otras opciones que son escala de grises que lo convierte a blanco y negro, podemos también ver los canales de RGB de la cámara entonces podemos hacer esta serie de cambios en esta cámara con la aplicación.

[![image](https://user-images.githubusercontent.com/108105124/201499455-e0d3ffef-16f0-459d-aa1c-c5142e01798a.png)](https://user-images.githubusercontent.com/108105124/201499455-e0d3ffef-16f0-459d-aa1c-c5142e01798a.png)  [![image](https://user-images.githubusercontent.com/108105124/201499461-a7efc444-2cb5-449b-b174-ff58c0ef75f0.png)](https://user-images.githubusercontent.com/108105124/201499461-a7efc444-2cb5-449b-b174-ff58c0ef75f0.png)  [![image](https://user-images.githubusercontent.com/108105124/201499462-25e9fc87-9e9d-4d2f-921e-3195d74bbcef.png)](https://user-images.githubusercontent.com/108105124/201499462-25e9fc87-9e9d-4d2f-921e-3195d74bbcef.png)  [![image](https://user-images.githubusercontent.com/108105124/201499464-0d0aa32d-8680-454e-8927-63c578cd43ac.png)](https://user-images.githubusercontent.com/108105124/201499464-0d0aa32d-8680-454e-8927-63c578cd43ac.png)  [![image](https://user-images.githubusercontent.com/108105124/201499468-52955596-ee39-4108-a95f-d2f7fdee6b9b.png)](https://user-images.githubusercontent.com/108105124/201499468-52955596-ee39-4108-a95f-d2f7fdee6b9b.png)  [![image](https://user-images.githubusercontent.com/108105124/201499469-b7693bab-217f-4663-bba3-6d5efc8f3038.png)](https://user-images.githubusercontent.com/108105124/201499469-b7693bab-217f-4663-bba3-6d5efc8f3038.png)

Observamos que por default tiene en automático la AWB Gain que por lo que vemos en la cámara es la ganancia de colores en la imagen de ejemplo al estar desactivada.

[![image](https://user-images.githubusercontent.com/108105124/201499477-2f11f728-1d0c-4ef2-b48f-2a85b4ed902a.png)](https://user-images.githubusercontent.com/108105124/201499477-2f11f728-1d0c-4ef2-b48f-2a85b4ed902a.png)

En la aplicación de la cámara podemos ver que tiene la opción de poner filtros como podemos ver en los ejemplos los filtros son Sunny, Office, Cloudy y Home estos son los que tiene la aplicación.

[![image](https://user-images.githubusercontent.com/108105124/201499479-3f2ceb40-de5c-4072-b153-94bb50330af3.png)](https://user-images.githubusercontent.com/108105124/201499479-3f2ceb40-de5c-4072-b153-94bb50330af3.png)  [![image](https://user-images.githubusercontent.com/108105124/201499483-d77a13b1-e207-4109-8829-32f798b342a0.png)](https://user-images.githubusercontent.com/108105124/201499483-d77a13b1-e207-4109-8829-32f798b342a0.png)  [![image](https://user-images.githubusercontent.com/108105124/201499485-29ab6a52-edcf-4c49-8664-cad18950ce2c.png)](https://user-images.githubusercontent.com/108105124/201499485-29ab6a52-edcf-4c49-8664-cad18950ce2c.png)  [![image](https://user-images.githubusercontent.com/108105124/201499488-47b7ccec-ed84-4c20-8ddc-bba821a85fca.png)](https://user-images.githubusercontent.com/108105124/201499488-47b7ccec-ed84-4c20-8ddc-bba821a85fca.png)

Aquí probamos otra opción el cual seria AEC DSP por lo que observamos ajusta automáticamente la luz y contraste esta desactivado por default por la cantidad de procesamiento que utiliza y vemos la lentitud de la cámara.

[![image](https://user-images.githubusercontent.com/108105124/201499493-86fcfabf-498f-4ffe-90b5-84524ac072a6.png)](https://user-images.githubusercontent.com/108105124/201499493-86fcfabf-498f-4ffe-90b5-84524ac072a6.png)

Aquí vemos que la opción AE Level es el brillo de la imagen se puede ajustar como queremos y beneficiamos lo que necesite la imagen.

[![image](https://user-images.githubusercontent.com/108105124/201499497-9b0ead89-9e0d-4ba0-b08c-c5ff05cfae12.png)](https://user-images.githubusercontent.com/108105124/201499497-9b0ead89-9e0d-4ba0-b08c-c5ff05cfae12.png)

Aquí vemos que nos aparece Exposure si desactivamos la opción del AEC SENSOR nos permite ajustarlo manualmente en este caso esta el máximo y aumento el brillo de esta en este caso lo volvimos a activar para nos diera la mejor configuración de la imagen.

[![image](https://user-images.githubusercontent.com/108105124/201499501-3d262973-9caa-4499-9c0a-1f83fc0f3521.png)](https://user-images.githubusercontent.com/108105124/201499501-3d262973-9caa-4499-9c0a-1f83fc0f3521.png)

En esta opción fue la más interesante con la que nos topamos al estar probando con las diferentes opciones que ofrece que seria en AGC esta activado por defecto pero por lo que podemos ver al desactivarlos es que entra un tipo interferencia en la imagen lo cual nos da un efecto para nuestras imágenes muy interesante.

[![image](https://user-images.githubusercontent.com/108105124/201499504-70c43ac7-db7a-4e06-8ed9-74eeb5961080.png)](https://user-images.githubusercontent.com/108105124/201499504-70c43ac7-db7a-4e06-8ed9-74eeb5961080.png)

En la aplicación nos permite también ajustar la ganancia de la luz, digamos que estamos en un lugar con demasiada luz natural y la imagen no la podemos ver con los mejores detalles esta opción nos permite ajustar esa ganancia y tener un mejor ajuste de luz.

[![image](https://user-images.githubusercontent.com/108105124/201499509-5d2a43a6-f7da-4619-bf6d-cb15511c5b24.png)](https://user-images.githubusercontent.com/108105124/201499509-5d2a43a6-f7da-4619-bf6d-cb15511c5b24.png)

En esta opción notamos que tenemos el RAW GMA desactivado por default al activarlo observamos que ajusta ciertos parámetros automáticamente para que la imagen se ve mejor.

[![image](https://user-images.githubusercontent.com/108105124/201499514-37e4ce3d-2801-4194-be28-947a226c495e.png)](https://user-images.githubusercontent.com/108105124/201499514-37e4ce3d-2801-4194-be28-947a226c495e.png)

En esta aplicación también tiene efectos en la cámara por ejemplo aquí vemos que la cámara esta volteada como si fuera un espejo, esta al revés tiene una corrección de colores o pone las barras de colores en la imagen.

[![image](https://user-images.githubusercontent.com/108105124/201499516-4f4b5c09-792a-4b3f-8f3f-5111c52dcc68.png)](https://user-images.githubusercontent.com/108105124/201499516-4f4b5c09-792a-4b3f-8f3f-5111c52dcc68.png)  [![image](https://user-images.githubusercontent.com/108105124/201499518-e53b4f5f-4e9f-4e52-87a4-4589f88e467d.png)](https://user-images.githubusercontent.com/108105124/201499518-e53b4f5f-4e9f-4e52-87a4-4589f88e467d.png)  [![image](https://user-images.githubusercontent.com/108105124/201499520-196449b7-a26c-4153-a08f-f5a90904a50a.png)](https://user-images.githubusercontent.com/108105124/201499520-196449b7-a26c-4153-a08f-f5a90904a50a.png)  [![image](https://user-images.githubusercontent.com/108105124/201499525-b63fef7e-872d-4245-af16-3e40e43d8cf9.png)](https://user-images.githubusercontent.com/108105124/201499525-b63fef7e-872d-4245-af16-3e40e43d8cf9.png)

También tiene una opción de reconocimiento de imagen muy básica pero puede detectar caras la cámara donde podemos hacer un poco de programación y otras cosas que se tiene en la imagen.

[![image](https://user-images.githubusercontent.com/108105124/201499529-995dcecf-8fa3-4c0d-8d38-a3f14d37bae5.png)](https://user-images.githubusercontent.com/108105124/201499529-995dcecf-8fa3-4c0d-8d38-a3f14d37bae5.png)

 **Código fuente**

#include "esp_camera.h" #include <WiFi.h>

// // WARNING!!! PSRAM IC required for UXGA resolution and high JPEG quality // Ensure ESP32 Wrover Module or other board with PSRAM is selected // Partial images will be transmitted if image exceeds buffer size // // You must select partition scheme from the board menu that has at least 3MB APP space. // Face Recognition is DISABLED for ESP32 and ESP32-S2, because it takes up from 15 // seconds to process single frame. Face Detection is ENABLED if PSRAM is enabled as well

// =================== // Select camera model // =================== //#define CAMERA_MODEL_WROVER_KIT // Has PSRAM //#define CAMERA_MODEL_ESP_EYE // Has PSRAM //#define CAMERA_MODEL_ESP32S3_EYE // Has PSRAM //#define CAMERA_MODEL_M5STACK_PSRAM // Has PSRAM //#define CAMERA_MODEL_M5STACK_V2_PSRAM // M5Camera version B Has PSRAM //#define CAMERA_MODEL_M5STACK_WIDE // Has PSRAM //#define CAMERA_MODEL_M5STACK_ESP32CAM // No PSRAM //#define CAMERA_MODEL_M5STACK_UNITCAM // No PSRAM #define CAMERA_MODEL_AI_THINKER // Has PSRAM //#define CAMERA_MODEL_TTGO_T_JOURNAL // No PSRAM // ** Espressif Internal Boards ** //#define CAMERA_MODEL_ESP32_CAM_BOARD //#define CAMERA_MODEL_ESP32S2_CAM_BOARD //#define CAMERA_MODEL_ESP32S3_CAM_LCD

#include "camera_pins.h"

// =========================== // Enter your WiFi credentials // =========================== const char* ssid = "belkin54g"; const char* password = "raymundo";

void startCameraServer();

void setup() { Serial.begin(115200); Serial.setDebugOutput(true); Serial.println();

camera_config_t config; config.ledc_channel = LEDC_CHANNEL_0; config.ledc_timer = LEDC_TIMER_0; config.pin_d0 = Y2_GPIO_NUM; config.pin_d1 = Y3_GPIO_NUM; config.pin_d2 = Y4_GPIO_NUM; config.pin_d3 = Y5_GPIO_NUM; config.pin_d4 = Y6_GPIO_NUM; config.pin_d5 = Y7_GPIO_NUM; config.pin_d6 = Y8_GPIO_NUM; config.pin_d7 = Y9_GPIO_NUM; config.pin_xclk = XCLK_GPIO_NUM; config.pin_pclk = PCLK_GPIO_NUM; config.pin_vsync = VSYNC_GPIO_NUM; config.pin_href = HREF_GPIO_NUM; config.pin_sscb_sda = SIOD_GPIO_NUM; config.pin_sscb_scl = SIOC_GPIO_NUM; config.pin_pwdn = PWDN_GPIO_NUM; config.pin_reset = RESET_GPIO_NUM; config.xclk_freq_hz = 20000000; config.frame_size = FRAMESIZE_UXGA; config.pixel_format = PIXFORMAT_JPEG; // for streaming //config.pixel_format = PIXFORMAT_RGB565; // for face detection/recognition config.grab_mode = CAMERA_GRAB_WHEN_EMPTY; config.fb_location = CAMERA_FB_IN_PSRAM; config.jpeg_quality = 12; config.fb_count = 1;

// if PSRAM IC present, init with UXGA resolution and higher JPEG quality // for larger pre-allocated frame buffer. if(config.pixel_format == PIXFORMAT_JPEG){ if(psramFound()){ config.jpeg_quality = 10; config.fb_count = 2; config.grab_mode = CAMERA_GRAB_LATEST; } else { // Limit the frame size when PSRAM is not available config.frame_size = FRAMESIZE_SVGA; config.fb_location = CAMERA_FB_IN_DRAM; } } else { // Best option for face detection/recognition config.frame_size = FRAMESIZE_240X240; #if CONFIG_IDF_TARGET_ESP32S3 config.fb_count = 2; #endif }

#if defined(CAMERA_MODEL_ESP_EYE) pinMode(13, INPUT_PULLUP); pinMode(14, INPUT_PULLUP); #endif

// camera init esp_err_t err = esp_camera_init(&config); if (err != ESP_OK) { Serial.printf("Camera init failed with error 0x%x", err); return; }

sensor_t * s = esp_camera_sensor_get(); // initial sensors are flipped vertically and colors are a bit saturated if (s->id.PID == OV3660_PID) { s->set_vflip(s, 1); // flip it back s->set_brightness(s, 1); // up the brightness just a bit s->set_saturation(s, -2); // lower the saturation } // drop down frame size for higher initial frame rate if(config.pixel_format == PIXFORMAT_JPEG){ s->set_framesize(s, FRAMESIZE_QVGA); }

#if defined(CAMERA_MODEL_M5STACK_WIDE) || defined(CAMERA_MODEL_M5STACK_ESP32CAM) s->set_vflip(s, 1); s->set_hmirror(s, 1); #endif

#if defined(CAMERA_MODEL_ESP32S3_EYE) s->set_vflip(s, 1); #endif

WiFi.begin(ssid, password); WiFi.setSleep(false);

while (WiFi.status() != WL_CONNECTED) { delay(500); Serial.print("."); } Serial.println(""); Serial.println("WiFi connected");

startCameraServer();

Serial.print("Camera Ready! Use 'http://"); Serial.print(WiFi.localIP()); Serial.println("' to connect"); }

void loop() { // Do nothing. Everything is done in another task by the web server delay(10000); }

**Conclusiones:** En conclusión podemos ver todas las opciones que nos ofrece la cámara ESP32 y las oportunidades de programación que esta ofrece es muy interesante lo que una cámara pequeña puede ofrecer sin necesidad de tener cámaras demasiado caras en nuestro a ver el potencial de programación y de aplicaciones que se pueden hacer es demasiado grande que nos podemos volver muy creativos con la cámara es demasiado grande y muy interesante para ser realista pero dependerá de nuestro potencial y provecho que le saquemos a la aplicación que dictara lo que es mejor.



