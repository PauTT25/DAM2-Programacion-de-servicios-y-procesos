1. Introducción

El procesamiento de imágenes es una tarea que puede requerir bastante tiempo y recursos del ordenador, especialmente cuando trabajamos con fotografías de gran resolución. Por ejemplo, aplicar filtros, modificar colores o realizar transformaciones sobre millones de píxeles puede provocar que el programa tarde demasiado y que la interfaz deje de responder mientras se realiza el trabajo. Por este motivo, hemos desarrollado un procesador de imágenes que divide una fotografía en pequeños bloques y reparte su procesamiento entre varios trabajadores, con el objetivo de aprovechar mejor los recursos del equipo, reducir los tiempos de espera y permitir que el usuario siga interactuando con la aplicación.


2. ¿Para qué sirve el programa?

El programa está pensado para cualquier persona que necesite aplicar modificaciones a imágenes de forma sencilla y visualizar cómo se procesan. Permite seleccionar una fotografía, dividirla en bloques de diferentes tamaños y elegir cuántos trabajadores se encargarán de procesarla. También permite seleccionar distintos efectos, como invertir los colores, convertir la imagen a escala de grises, aplicar sepia, aumentar el brillo o modificar el contraste.

Una de sus principales ventajas es que el trabajo se distribuye entre varios Web Workers, que procesan diferentes partes de la imagen de manera concurrente. Además, el usuario puede elegir el orden en el que se procesan los bloques, consultar el porcentaje completado, controlar el proceso mediante las opciones de pausa, reanudación y cancelación, y descargar el resultado final. Esto permite experimentar con diferentes configuraciones y comprobar cómo influyen el tamaño de los bloques y el número de trabajadores en el procesamiento.


3. Cuestiones técnicas del proyecto

La aplicación se ha desarrollado utilizando HTML, CSS y JavaScript. HTML define la estructura de la interfaz, CSS se encarga de su diseño y JavaScript controla el procesamiento de la imagen mediante el elemento Canvas. La parte principal está organizada mediante una clase llamada ProcesadorImagen, que se encarga de dividir la fotografía en bloques, crear los trabajadores y repartir las tareas. Para conseguir el procesamiento concurrente se utilizan Web Workers, que ejecutan operaciones independientemente del hilo principal del navegador. Cada trabajador recibe los píxeles de un bloque mediante postMessage(), aplica el efecto seleccionado y devuelve el resultado para que el hilo principal actualice el Canvas. Se utilizan mecanismos de comunicación y transferencia de datos, como postMessage(), onmessage y los ArrayBuffer, evitando tener que copiar innecesariamente los datos de los píxeles.

En cuanto a la verificación, la aplicación incorpora controles para detectar errores al cargar las imágenes, gestionar los fallos de los trabajadores y mostrar el progreso del procesamiento. También permite comparar diferentes configuraciones, como utilizar uno, dos, cuatro u ocho Workers. Para su ejecución no necesita un servidor de base de datos ni dependencias externas, ya que funciona directamente en un navegador compatible con Web Workers. Como posible mejora, se podría incorporar una medición más completa del rendimiento, realizar pruebas sistemáticas con diferentes imágenes y añadir una comparación entre el procesamiento secuencial y el paralelo. Si se utiliza inteligencia artificial durante el desarrollo, puede servir como apoyo para generar o revisar partes del código, pero es necesario comprobar manualmente que los resultados sean correctos.

4. Despedida, cierre y resumen

Con este proyecto hemos desarrollado una aplicación capaz de procesar imágenes mediante la división del trabajo en bloques y la utilización de varios Web Workers. Hemos podido aplicar conceptos de programación concurrente y paralela, comunicación entre hilos, transferencia de información y coordinación de tareas. Además, hemos creado una interfaz que permite modificar diferentes parámetros y observar los resultados del procesamiento. Aunque la aplicación cumple su objetivo principal, todavía se puede mejorar incorporando estadísticas más detalladas, comparaciones de rendimiento y nuevas operaciones sobre imágenes. En definitiva, el proyecto demuestra cómo dividir una tarea grande en tareas más pequeñas permite aprovechar mejor los recursos del ordenador y desarrollar aplicaciones más eficientes.


Criterio	Parte del proyecto que lo demuestra
a) Programación concurrente	Los diferentes Workers procesan bloques de la imagen independientemente.
b) Paralela y distribuida	Se aplica paralelismo mediante Workers dentro del navegador. No es un sistema distribuido entre varios ordenadores.
c) Procesos y sistema operativo	El navegador y el sistema operativo gestionan los recursos y la ejecución de los Workers.
d) Hilos de ejecución	Cada Worker tiene un contexto de ejecución independiente del hilo principal.
e) Clases y subprocesos	La clase ProcesadorImagen crea y administra los Web Workers.
f) Compartir información	postMessage() envía los datos de cada bloque a los Workers.
g) Sincronización y resultados	onmessage recibe los resultados y el hilo principal actualiza el Canvas y el progreso.
h) Varias tareas en paralelo	Se reparten múltiples bloques entre varios Workers.
i) Depuración y documentación	Se controlan errores de carga y ejecución y se muestran mensajes de estado.


Importante: no afirmes que utilizar ocho Workers siempre será más rápido que utilizar uno. La creación de trabajadores, la transferencia de píxeles y la coordinación también tienen un coste. Precisamente, medir ese comportamiento demostraría que entiendes el funcionamiento de la programación paralela y no solamente cómo utilizarla.