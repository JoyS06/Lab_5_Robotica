# Lab_5_Robotica

# Integrantes: 
-Joyner Stiven Caballero Abril.
-Juan Felipe Triana Aguilera

# Introduccion: 

Este laboratorio tiene como objetivo principal determinar el modelo cinemático inverso del robot Phantom X y generar trayectorias de trabajo a partir de dicho modelo. Además, se busca implementar el modelo en MATLAB o Python y operar el robot mediante ROS utilizando las trayectorias generadas.

La cinemática inversa es un problema fundamental en robótica que consiste en determinar la configuración articular de un manipulador, dadas la posición y orientación del efector final respecto a la base. Para el robot Phantom X, que posee 4 grados de libertad, se combinan métodos geométricos con el desacople de muñeca para resolver este problema.

El laboratorio incluye una serie de ejercicios prácticos que abarcan desde el desarrollo e implementación del modelo cinemático inverso hasta la operación del robot en tareas de escritura sobre una superficie plana. A lo largo del informe se describirán los pasos seguidos, los resultados obtenidos y las conclusiones derivadas de la experimentación. Además, se proporcionarán detalles sobre los requisitos técnicos, el uso de herramientas específicas y la interacción con el usuario mediante una interfaz HMI (Human-Machine Interface).

# Objetivos:
• Determinar el modelo cinemático inverso del robot Phantom X.
• Generar trayectorias de trabajo a partir del modelo cinemático inverso del robot.
• Implementar el modelo cinemático inverso del robot en MATLAB o Python.
• Operar el robot usando ROS a partir de trayectorias generadas en MATLAB o Python.

# Desarrollo

![robot general](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/bb264ba2-4ac9-4769-a004-101123d33fef)

El primer paso para la elaboración de este laboratorio fue tomar las medidas de los eslabones del robot Phantom X Pincher. Para ello, se midió la distancia de junta a junta utilizando un calibrador. 

L1 = 10.5 cm 
L2 = 10.5 cm 
L3 = 6.5 cm 
L4 = 8 cm 

![robot general dh](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/6ed81aef-5e16-4265-8f5b-dca26d63d667)

Para simplificar la determinación de los ángulos del robot pincher, se analiza el vector de la muñeca en lugar del vector de la herramienta. Se reconoce que el vector de la muñeca es equivalente al vector de la herramienta menos un desplazamiento 𝐿 en la dirección de 𝑎. Esta aproximación facilita el proceso de cálculo al reducir la complejidad asociada con la posición y orientación del efector final. Al considerar únicamente el desplazamiento en la dirección especificada, se pueden obtener los ángulos necesarios de manera más eficiente y precisa, mejorando así el control y la operabilidad del robot.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/79000e86-9d96-4d57-b128-908165ca75f3)

Una forma de resolver este problema es aplicar la regla del paralelogramo para sumar vectores. Si dibujamos el vector tool y el vector \( L \) que representa el desplazamiento de la muñeca, podemos obtener el vector de la muñeca como la diagonal del paralelogramo formado por estos dos vectores. Así, se reconoce que el vector de la muñeca es el mismo vector tool menos un desplazamiento \( L \) en la dirección de \( a \).

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/d41c826a-ca85-4c1e-8eac-f90c35fa5724)

Para determinar el ángulo 1, se utiliza la geometría del triángulo formado por el eje del robot, el punto de contacto con el suelo y el centro de la cámara. Se aplica el teorema de Pitágoras y la ley de cosenos para obtener el valor del ángulo 1 en función de las dimensiones del robot y la distancia al objetivo.

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/df7fbddb-6502-4ede-a870-b7f64fc6427d)

![image](https://github.com/JoyS06/Lab_5_Robotica/assets/105253521/3bc0116f-1f7b-467c-aad4-bd766bfe5edd)

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




