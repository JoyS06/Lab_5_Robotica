# Lab_5_Robotica

# Integrantes: 
-Joyner Stiven Caballero Abril.

# Introduccion: 

Este laboratorio tiene como objetivo principal determinar el modelo cinemático inverso del robot Phantom X y generar trayectorias de trabajo a partir de dicho modelo. Además, se busca implementar el modelo en MATLAB o Python y operar el robot mediante ROS utilizando las trayectorias generadas.

La cinemática inversa es un problema fundamental en robótica que consiste en determinar la configuración articular de un manipulador, dadas la posición y orientación del efector final respecto a la base. Para el robot Phantom X, que posee 4 grados de libertad, se combinan métodos geométricos con el desacople de muñeca para resolver este problema.

El laboratorio incluye una serie de ejercicios prácticos que abarcan desde el desarrollo e implementación del modelo cinemático inverso hasta la operación del robot en tareas de escritura sobre una superficie plana. A lo largo del informe se describirán los pasos seguidos, los resultados obtenidos y las conclusiones derivadas de la experimentación. Además, se proporcionarán detalles sobre los requisitos técnicos, el uso de herramientas específicas y la interacción con el usuario mediante una interfaz HMI (Human-Machine Interface).

# Objetivos:
Determinar el modelo cinemático inverso del robot Phantom X.

Generar trayectorias de trabajo a partir del modelo cinemático inverso del robot.

Implementar el modelo cinemático inverso del robot en MATLAB o Python.

Operar el robot usando ROS a partir de trayectorias generadas en MATLAB o Python.

# Desarrollo

![robot general](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/bb264ba2-4ac9-4769-a004-101123d33fef)

El primer paso para la elaboración de este laboratorio fue tomar las medidas de los eslabones del robot Phantom X Pincher. Para ello, se midió la distancia de junta a junta utilizando un calibrador. 

![robot general dh](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/6ed81aef-5e16-4265-8f5b-dca26d63d667)

Para simplificar la determinación de los ángulos del robot pincher, se analiza el vector de la muñeca en lugar del vector de la herramienta. Se reconoce que el vector de la muñeca es equivalente al vector de la herramienta menos un desplazamiento 𝐿 en la dirección de 𝑎. Esta aproximación facilita el proceso de cálculo al reducir la complejidad asociada con la posición y orientación del efector final. Al considerar únicamente el desplazamiento en la dirección especificada, se pueden obtener los ángulos necesarios de manera más eficiente y precisa, mejorando así el control y la operabilidad del robot.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/79000e86-9d96-4d57-b128-908165ca75f3)

Una forma de resolver este problema es aplicar la regla del paralelogramo para sumar vectores. Si dibujamos el vector tool y el vector \( L \) que representa el desplazamiento de la muñeca, podemos obtener el vector de la muñeca como la diagonal del paralelogramo formado por estos dos vectores. Así, se reconoce que el vector de la muñeca es el mismo vector tool menos un desplazamiento \( L \) en la dirección de \( a \).

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/f5b7ffc2-ebc0-48ea-8ecd-0294152dedc4)

Para determinar el ángulo 1, se utiliza la geometría del triángulo formado por el eje del robot, el punto de contacto con el suelo y el centro de la cámara. Se aplica el teorema de Pitágoras y la ley de cosenos para obtener el valor del ángulo 1 en función de las dimensiones del robot y la distancia al objetivo.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/df7fbddb-6502-4ede-a870-b7f64fc6427d)

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/f847e058-b197-4276-93a3-cbfd58a5b0ae)

Se examina la vista lateral del robot para determinar los ángulos theta2 y theta3, utilizando la geometría del sistema y las posiciones relativas de los componentes para calcular con precisión estos ángulos. 

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/847dded5-faf7-4d7a-ab8d-6831895d40cc)

Se halla un pw2 auxiliar para hallar estos angulos mas facilmente

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/ee42bfb3-7c64-471e-9074-60a8c129ccb3)

Con este PW2 se halla primero el ángulo theta3 con la ley del coseno

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/7cd558a7-3adf-4fa5-90ea-89c0504608b5)

Se procede a determinar el ángulo theta2 analizando la vista lateral del sistema. Para ello, se emplea la ley de cosenos junto con los ángulos alpha y psi definidos en la figura adjunta. Este enfoque permite derivar una expresión para theta2 en términos de las longitudes de los eslabones y los ángulos mencionados, facilitando así la resolución del problema de cinemática inversa al proporcionar una relación matemática clara y precisa entre estos parámetros

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/701b4334-7448-47e7-a02e-4bd7965bb903)

Ahora se obtiene Theta2

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/85a07a90-a701-4ac3-92ca-54a37983d0e8)

# Trayectorias:

Para planificar las trayectorias, inicialmente se realizó un dibujo del espacio de trabajo utilizando el software Dynamixel Wizard. Se tomaron las medidas precisas del área de trabajo, y posteriormente se trazaron dos círculos con estas dimensiones en AutoCAD. Este enfoque permitió determinar con exactitud la ubicación de los puntos clave donde se llevarían a cabo las figuras deseadas. La combinación de estos métodos asegura una correcta representación y planificación de las trayectorias del robot, facilitando la ejecución precisa de las tareas programadas.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/3986e053-aed6-414e-81ee-06b924609476)

Para obtener los puntos, se colocaron las ubicaciones en AutoCAD sobre las trayectorias de las figuras y se extrajeron las coordenadas necesarias. Estas coordenadas se pasaron a Python como una lista de vectores con tres componentes (x, y, z). Las coordenadas z se ajustaron manualmente: cuando el robot estaba dibujando, el valor de z se mantenía en cero, y cuando había un salto en la trayectoria, el valor de z se incrementaba para levantar el marcador y evitar el dibujo. Para las letras, se utilizaron puntos específicos. Para el círculo, se estableció una posición inicial y, mediante una función, se trazó el círculo incrementando gradualmente el ángulo. Las figuras obtenidas se pueden observar en la siguiente imagen.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/95a6f086-ef26-40f3-8d7d-4fc64d6db554)

# Analisis del codigo 

Luego de importar las librerías, se procede a crear el modelo de Denavit-Hartenberg estándar (DHstd) del robot Phantom X Pincher utilizando la librería roboticstoolbox. Se definen las cuatro articulaciones revolutas del manipulador, especificando los parámetros DH correspondientes: el desplazamiento d, el ángulo alpha, el desplazamiento a y el ángulo theta.

Además, se utilizan las librerías cv2 y matplotlib.pyplot para mostrar y visualizar las imágenes que representan las trayectorias del marcador, permitiendo así una mejor comprensión y análisis del comportamiento del robot.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/d24c63ed-4d87-4fe0-8be6-df7c46b2d47c)

En la función de cinemática inversa, se definen las longitudes de los eslabones del robot (l1 y l2), junto con algunas variables auxiliares (xaux y zaux) que se utilizan repetidamente durante la ejecución de la función. Los valores de las distintas articulaciones se calculan en términos de arcotangentes, comenzando por el ángulo de la tercera articulación (theta3), seguido del cálculo del ángulo de la segunda articulación (theta2) y luego el ángulo de la primera articulación (theta1). Finalmente, se calcula el ángulo de la cuarta articulación (theta4), que no se resuelve de manera geométrica. Todos estos valores se devuelven como una lista.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/d0cec4de-f05f-45ef-8a1b-2b8219e38407)

La función enviarPosicion se encarga de enviar distintas posiciones al controlador del manipulador Phantom X Pincher. A continuación, se detallan los pasos y componentes de esta función:

1 Creación del objeto Publisher: Se crea un objeto Publisher de ROS que se encarga de enviar mensajes al tópico /joint_trajectory para controlar el robot. Este objeto se inicializa con el tipo de mensaje JointTrajectory.

2 Inicialización del nodo de ROS: Se inicia un nodo de ROS llamado joint_publisher, que permite la comunicación entre el código de Python y el robot.

3 Ciclo de iteración sobre los puntos: Se utiliza un bucle for para iterar sobre la lista de puntos ingresados como parámetro. Cada punto se descompone en sus coordenadas X, Y y Z.

4 Creación de objetos de mensajes:

- Se crea un objeto state de tipo JointTrajectory que contendrá el mensaje a publicar.
- Se crea un objeto point de tipo JointTrajectoryPoint que representará un punto específico en la trayectoria de las articulaciones.

5 Cálculo de la cinemática inversa: La función cinemInversa se utiliza para obtener los valores de las articulaciones correspondientes a las coordenadas X, Y y Z del punto actual. Estos valores se almacenan en la variable posActual.

6 Ajuste de la posición actual: Dependiendo del valor de la variable flag, se ajusta el valor de la cuarta articulación en posActual.

7 Actualización del mensaje:

- Los valores de las articulaciones se asignan a la variable point.
- La variable point se añade a la lista de puntos en state.
- El mensaje state se publica utilizando el objeto Publisher creado anteriormente.

8 Pausa del programa: Finalmente, se suspende la ejecución del programa brevemente utilizando rospy.sleep(3) para dar tiempo al robot a ejecutar la instrucción.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/2fcde105-1fe7-418d-a7f1-0668c192e252)

Similar a la función anterior, enviarAngulos crea un objeto Publisher con el tópico /joint_trajectory, utilizando el mensaje de tipo JointTrajectory. A continuación, se inicializa el nodo de ROS y se crea el objeto state de la clase JointTrajectory. Dentro de este objeto state, se define un objeto point de la clase JointTrajectoryPoint.

Los ángulos recibidos como parámetros de entrada en la función se asignan a la variable positions del objeto point. Este objeto point se añade posteriormente al objeto state, que contiene la trayectoria completa de las articulaciones del robot. Finalmente, el objeto state se publica mediante el Publisher, y se deja un breve tiempo de espera para asegurar la correcta ejecución de los comandos por parte del robot.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/b85a9a88-3cf3-43f7-aa02-576e142e70b5)

La función joint_publisher establece la posición de home para el robot y realiza una serie de movimientos mediante la función enviarPosicion. A continuación, se describe el proceso en detalle:

1 Establecimiento de la posición de home: Se define una posición de home para el robot en la variable posicionHome. Esta posición se envía al robot utilizando la función enviarAngulos.

2 Movimientos iniciales:

- Se define una lista de puntos que representan el espacio de trabajo del robot.
- La función enviarPosicion se utiliza para mover el robot a estos puntos. Primero, el robot se lleva al punto donde está el marcador, lo recoge y luego se levanta para volver a la posición de home.

3 Ciclo while para interacción con el usuario:

- Se inicia un ciclo while que permanecerá activo mientras el programa esté en ejecución.
- Durante este ciclo, se muestra un menú al usuario con diferentes opciones de tareas a realizar: dibujar el espacio de trabajo, dibujar las iniciales de los nombres, dibujar un círculo, dibujar una X sobre el círculo, o salir del programa.
- El usuario debe ingresar el número correspondiente a la tarea deseada, y el programa ejecutará la función correspondiente.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/8e7e9122-d6bf-4853-8c7a-3f68986361c3)

Para el desarrollo de distintas tareas, se sigue un procedimiento similar en cada caso. Primero, se muestra una imagen que ilustra al usuario la trayectoria teórica que seguirá el robot. Luego, se define una lista de puntos que representa el recorrido que debe seguir el marcador, con cada uno de estos puntos especificado en sus coordenadas X, Y y Z. Esta lista de puntos se envía a la función enviarPosicion, que se encarga de controlar el recorrido del robot.

Durante la ejecución, se mide y muestra el tiempo total de la tarea en la consola. Una vez completado el recorrido, el robot regresa a la posición de home. Este procedimiento asegura que el robot siga las trayectorias deseadas de manera precisa y eficiente, proporcionando retroalimentación en tiempo real al usuario sobre la duración de cada tarea.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/b9ecbc36-df52-4f1d-a58d-5bff178e1985)

El bloque final del código se asegura de que la función joint_publisher() se ejecute solo cuando el script se ejecuta como programa principal. Utilizando la condición if __name__ == '__main__':, se verifica que el script no se esté importando como módulo. Dentro de este bloque, se utiliza un try para intentar ejecutar la función principal después de una breve pausa de 1 segundo (time.sleep(1)), permitiendo así que todas las inicializaciones necesarias se completen. Si se produce una interrupción de ROS (rospy.ROSInterruptException), el except captura esta excepción y simplemente la ignora con pass, asegurando que el programa termine de manera limpia sin realizar ninguna acción adicional.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/3bcdc515-ac4b-4cce-bf9f-08b71bddf9b6)

# Resultado

En el siguiente video podemos ver los resultados obtenidos:

https://www.youtube.com/watch?v=DuJOaEzIpIs

Para medir los dibujos realizados por el robot, se puede establecer una regla de proporción entre la longitud real y la longitud en píxeles. Si la tabla mide aproximadamente 50 cm y la imagen tiene una longitud de 273750 píxeles, entonces cada 10 píxeles equivalen a 1.826 mm en la realidad. Utilizando esta proporción y las herramientas de medición de píxeles que ofrece el programa Paint, que proporcionan la longitud en horizontal y vertical en píxeles, es posible calcular la distancia en píxeles entre dos puntos de la imagen. Aplicando el teorema de Pitágoras a estas mediciones, se puede convertir la distancia en píxeles a milímetros. Esta metodología permite obtener medidas precisas de los distintos dibujos realizados por el robot en términos de longitud real, asegurando así una representación exacta de las dimensiones en el mundo físico y finalmente, mediante las longitudes teóricas con las que se planteo el ejercicio se obtiene el error relativo para cada una de las medidas.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/ca095c55-2c85-4425-874e-cfec2a6b8f59)

# Conclusiones

1 Utilidad de la Cinemática Inversa: La cinemática inversa es una herramienta esencial para la programación del robot Pincher. Permite definir trayectorias complejas mediante ecuaciones simples, facilitando el diseño de movimientos precisos y controlados con un bajo consumo de recursos computacionales. Esta capacidad es crucial para aplicaciones que requieren alta precisión y eficiencia.

2 Limitaciones Estructurales: A pesar de las ventajas de la cinemática inversa, es importante considerar las limitaciones estructurales del robot Pincher. Durante el movimiento, el Pincher puede generar vibraciones que afectan la precisión de las trayectorias. Estas vibraciones son una consecuencia de la rigidez y el diseño del robot, y deben ser tenidas en cuenta al planificar y ejecutar movimientos.

3 Errores en Geometrías Complejas: Al comparar las dimensiones teóricas con las reales en tareas que involucran geometrías complejas, como las letras, se observa un mayor porcentaje de error. Este error es más significativo en comparación con figuras más simples, como círculos y líneas. Sin embargo, incluso en estas figuras simples, se pueden notar imperfecciones en las geometrías curvas, como en el caso del círculo, donde un lado puede ser ligeramente más largo que el otro.
