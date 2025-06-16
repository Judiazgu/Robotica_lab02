# Robotica_lab02


## INTRODUCCION

Este proyecto consiste en la simulación y ejecución real de la decoración automatizada de una torta utilizando un robot ABB IRB 140. Se programaron trayectorias personalizadas, se diseñó una herramienta de escritura, y se controlaron entradas/salidas digitales y una banda transportadora.

## OBJETIVOS

- Diseñar y calibrar una herramienta para el robot.

- Programar trayectorias de escritura y decoración en RAPID.

- Utilizar y calibrar un workobject para cambiar el contexto de trabajo.

- Implementar el control por entradas y salidas digitales.

- Simular y ejecutar el proceso en RobotStudio y robot físico.

## DESCRIPCION DE LA SOLUCION PLANTEADA

Para resolver el reto del Laboratorio 2 de Robótica Industrial, planteamos una solución que simula la decoración automatizada de una torta virtual utilizando un robot ABB IRB 140, programado en RobotStudio con el lenguaje RAPID.

La idea principal fue crear un sistema que, a través de trayectorias bien definidas, pudiera escribir sobre una superficie plana los nombres de los integrantes del grupo, como si fuera una decoración de pastel. También incorporamos el uso de entradas y salidas digitales para que el proceso fuera más automatizado.

### Etapas del desarrollo

1. **Diseño de la herramienta (TCP)**  
   Diseñamos una herramienta para simular un marcador que va fijado al robot. 

2. **Definición del entorno de trabajo (Workobject)**  
   Se creó un `workobject` que representa la torta. Todo el movimiento del robot se programó respecto a ese sistema de coordenadas, lo cual permite precisión en la decoración.

3. **Programación de trayectorias por letra**  
   Para cada letra de los nombres se creó un procedimiento (`PROC`) con movimientos `MoveJ`, `MoveL` y `MoveC`. Por ejemplo, la `J` está en `Path_30`, la `U` en `Path_40`, y así sucesivamente. Estas trayectorias dibujan cada letra directamente sobre la superficie.

4. **Lógica de control con entradas y salidas digitales**  
   Se utilizó una estructura `WHILE` que espera una señal de inicio (`DI_01`) para activar una luz de estado (`DO_02`). Luego, otra señal (`Sens_01`) indica que la torta está en posición, y el robot comienza a ejecutar todas las trayectorias en orden. Al final, se activa una salida digital (`END_TASK`) que indica que la decoración terminó.

5. **Secuencia y retorno al home**  
   El robot inicia en la posición `HOME`, realiza todas las trayectorias de forma continua, y regresa a `HOME` al final del proceso. También se utilizan trayectorias de entrada y salida para cada letra (subiendo y bajando el marcador con coordenadas en z).

6. **Señales digitales para control adicional**  
   Dejamos listas las salidas para que puedan conectarse a otros elementos como bandas transportadoras, luces o alarmas, en caso de que se quiera extender el sistema.


Este desarrollo cumple con los objetivos del laboratorio, ya que integra el uso de trayectorias, trabajo con herramientas personalizadas, sistema de coordenadas, programación en RAPID, y manejo de entradas/salidas digitales.


## DISEÑO DE LA HERRAMIENTA

Inicialmente se planteo que la herramienta a utilizar sera un holder para un marcador borrable, lo que emulara el dosificador de material comestible para hacer figuras sobre los pasteles.

Dado lo anterior por medio del software Autodesk Inventor para el modelado de elementos, se planteo la geometria que debia tener esta herramienta. Se tuvo en cuenta que el angulo que debia tener la punta del marcador debe tener un angulo con respecto al flanche del robot, debido a que esto evitara que surgan distintas singularidares para el movimiento del brazo robotico. 

Por otra parte se realizaron las medidas del marcador para plantear las dimensiones del holder, ademas se añadio un resorte para que el marcador pueda oprimirse y pueda escribir. Ademas el resorte nos ayuda a que la herramienta y el robot no sufran un daño por culpa de los errores humanos de calibracion que existen dentro el proceso.

Por ultimo se realizo una revision sobre las caracteristicas y geometricas del flanche del robot, para tener las medidas exactas de los agujeros donde se colocaran los tornillos (en este caso M6) para el acople de los tornillos, y la longitud de estos tornillos. Ademas se calibró para que el extremo del marcador coincidiera con el punto que hace contacto con la torta virtual.

## ACCIONES DEL ROBOT

![Diagrama de flujo](/Media/Diagrama_de_flujo_Robot.png)

## FUNCIONES UTILIZADAS

A continuación, se describen las funciones utilizadas en el código RAPID implementado para el desarrollo del laboratorio de robótica industrial:

| Función          | Descripción                                                                 | Aplicación en el proyecto                                                  |
|------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------|
| `MoveJ`          | Realiza un movimiento articular (por ángulos de las juntas del robot).      | Utilizada para ir a posiciones iniciales o finales con movimientos suaves. |
| `MoveL`          | Realiza un movimiento lineal entre dos puntos en el espacio cartesiano.     | Usada para trazar líneas rectas (letras o formas decorativas).             |
| `MoveC`          | Realiza un movimiento curvo entre dos puntos con un punto intermedio.       | Utilizada para trazar curvas o arcos en letras como la “J” o la “S”.       |
| `SetDO`          | Establece una salida digital a "1" (activar señal).                         | Enciende dispositivos como luces o bandas transportadoras.                 |
| `ResetDO`        | Establece una salida digital a "0" (desactivar señal).                      | Apaga señales previamente activadas.                                       |
| `WHILE ... DO`   | Bucle que repite acciones mientras se cumpla una condición.                | Mantiene el sistema en espera hasta recibir entradas digitales.            |
| `IF ... THEN`    | Condicional que ejecuta un bloque si se cumple una condición.              | Controla el flujo según las señales de entrada (`DI_01`, `Sens_01`).       |
| `CONST`          | Define constantes (como posiciones `robtarget`) que no cambian en ejecución.| Define coordenadas fijas para letras, HOME y trayectorias.                 |
| `PROC`           | Define un procedimiento o subrutina en RAPID.                              | Cada trayectoria (letra o figura) está organizada como un `PROC` distinto. |
| `MODULE`         | Contenedor principal del código RAPID.                                     | Organiza todas las funciones, trayectorias y configuraciones.              |
| `PERS`           | Define variables persistentes (que conservan su valor).                    | Usado en la herramienta (`TCP_TOOL`) y el objeto de trabajo (`Workobject_1`). |
| `TASK PERS`      | Define variables persistentes específicas por tarea.                       | Aplica a `Workobject_1`, usado en la referencia del entorno.               |


## PLANO DE PLANTA

## SIMULACION

[![Watch the video](https://img.youtube.com/vi/pgdmwPn4A4Y/maxresdefault.jpg)](https://youtu.be/pgdmwPn4A4Y)
https://youtu.be/pgdmwPn4A4Y

## IMPLEMENTACION

[![Watch the video](https://img.youtube.com/vi/s4zlZOmxGf4/maxresdefault.jpg)](https://youtu.be/s4zlZOmxGf4)
https://youtu.be/s4zlZOmxGf4