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

Una manera de abordar este problema es emplear la regla del paralelogramo para la suma de vectores. Al dibujar el vector de la herramienta (tool) y el vector \(L\), que representa el desplazamiento de la muñeca, se puede obtener el vector de la muñeca como la diagonal del paralelogramo formado por estos dos vectores. De esta forma, se reconoce que el vector de la muñeca es el mismo vector de la herramienta menos un desplazamiento \(L\) en la dirección de \(a\).

\[ P_w = P_{TCP} - L_{4a} \]

Para determinar el ángulo 1, se utiliza la geometría del triángulo formado por el eje del robot, el punto de contacto con el suelo y el centro de la cámara. Aplicando el teorema de Pitágoras y la ley de cosenos, se puede obtener el valor del ángulo 1 en función de las dimensiones del robot y la distancia al objetivo. Esta metodología permite calcular de manera precisa los ángulos necesarios para posicionar la herramienta del robot en la ubicación deseada, facilitando así el control y la ejecución de tareas específicas.
