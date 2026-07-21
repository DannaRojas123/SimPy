# SimPy
## ¿Qué es SimPy?

Los ingenieros industriales y de sistemas están a cargo de muchos procesos en su carrera, y en ocasiones la cantidad de variables a controlar puede resultar abrumadora. SimPy es una biblioteca de Python que existe desde 2002 para modelar procesos en un formato simple, pensado para que nuevos programadores puedan aprenderlo y aplicarlo.

El entorno (Environment) es lo que permite que la simulación comience, ya que da seguimiento a todos los procesos que ocurren en el código. Debido a que controla el tiempo, primero se crea el entorno y se le agregan procesos; una vez que se ejecuta, el tiempo simulado avanza y se registra lo que ocurre con procesos, recursos, etc.

Para aprovechar el entorno es necesario entender los procesos, que son justamente lo que el entorno rastrea. Un proceso representa una acción que ocurre a lo largo del tiempo, y se pueden ejecutar varias a la vez dentro del mismo entorno (por ejemplo, para simular una línea de ensamblaje). Para escribir un proceso, primero se define (cuándo comienza el trabajo y cuánto tiempo toma) y después se ejecuta como proceso dentro del entorno.

## Características

SimPy es un marco de simulación de eventos discretos (DES) basado en procesos, escrito en Python. Permite modelar componentes activos del mundo real (como clientes o vehículos) usando funciones generadoras de Python.

<img width="682" height="531" alt="image" src="https://github.com/user-attachments/assets/93cf91c2-f8ed-4d31-a7a2-fc9232173705" />

## ¿Dónde se utiliza?
1. Modelado de procesos mediante funciones generadoras de Python
2. Gestión de recursos compartidos (servidores, contenedores, tiendas)
3. Programación y sincronización basada en eventos
4. Simulaciones en tiempo real sincronizadas con el reloj de pared
5. Seguimiento integral y recopilación de datos

## Ejemplos de uso en la vida real
<img width="696" height="381" alt="image" src="https://github.com/user-attachments/assets/54ac1116-97ac-49e5-8f73-c42090be8bd5" />

## Alternativas
Si se necesita una herramienta similar a SimPy, la mejor alternativa en Python puro es Salabim: es gratuita, corre completamente en Python y viene con animaciones y gráficos integrados. Para una visión más amplia existen herramientas basadas en R, o herramientas visuales de "arrastrar y soltar" como AnyLogic.

<img width="700" height="504" alt="image" src="https://github.com/user-attachments/assets/9f558dc9-4791-44df-b479-0a310bae06c5" />

## Resumen de los 3 ejemplos
<img width="680" height="184" alt="image" src="https://github.com/user-attachments/assets/949b6fb7-e8ca-40ba-bcfa-16363e6df55c" />
