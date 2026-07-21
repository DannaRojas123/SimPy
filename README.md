# SimPy

SimPy: Simulación de Eventos Discretos en Python
¿Qué es SimPy?

Los ingenieros industriales y de fabricación están a cargo de muchos procesos en su carrera, y en ocasiones la cantidad de variables a controlar puede resultar abrumadora. SimPy es una biblioteca de Python que existe desde 2002 para modelar procesos en un formato simple, pensado para que nuevos programadores puedan aprenderlo y aplicarlo.

El entorno (Environment) es lo que permite que la simulación comience, ya que da seguimiento a todos los procesos que ocurren en el código. Debido a que controla el tiempo, primero se crea el entorno y se le agregan procesos; una vez que se ejecuta, el tiempo simulado avanza y se registra lo que ocurre con procesos, recursos, etc.

Para aprovechar el entorno es necesario entender los procesos, que son justamente lo que el entorno rastrea. Un proceso representa una acción que ocurre a lo largo del tiempo, y se pueden ejecutar varias a la vez dentro del mismo entorno (por ejemplo, para simular una línea de ensamblaje). Para escribir un proceso, primero se define (cuándo comienza el trabajo y cuánto tiempo toma) y después se ejecuta como proceso dentro del entorno.

Características

SimPy es un marco de simulación de eventos discretos (DES) basado en procesos, escrito en Python. Permite modelar componentes activos del mundo real (como clientes o vehículos) usando funciones generadoras de Python.

Característica	Descripción
Simulación de eventos discretos (DES)	La simulación salta de un evento específico al siguiente, en lugar de avanzar milisegundo a milisegundo. Esto permite que los modelos corran muy rápido sin desperdiciar recursos en períodos inactivos.
Basado en Python	Al usar Python estándar, se puede aprovechar todo su ecosistema — por ejemplo, conectar pandas para entrada de datos y matplotlib para graficar resultados.
Orientado a procesos	En lugar de enfocarse en ecuaciones matemáticas globales, se escriben componentes activos (como un "cliente" que va a un banco) usando funciones generadoras. Simplemente se le indica al proceso qué hacer paso a paso y dónde esperar.
Gestión de recursos compartidos	Herramientas integradas para modelar limitaciones del mundo real: Resources (artículos con capacidad limitada, ej. 2 cajeros), Containers (cantidades continuas, ej. combustible), Stores (inventario de artículos discretos, ej. repuestos).
Ejecución de tiempo flexible	Se puede correr la simulación de tres formas: lo más rápido posible, en tiempo real (sincronizado con el reloj), o paso a paso (para depuración manual).
Sin GUI incorporada	SimPy es puramente una biblioteca de código; no incluye animación ni interfaz gráfica — la salida de datos y visualizaciones son responsabilidad del programador.
¿Dónde se utiliza?
Modelado de procesos mediante funciones generadoras de Python
Gestión de recursos compartidos (servidores, contenedores, tiendas)
Programación y sincronización basada en eventos
Simulaciones en tiempo real sincronizadas con el reloj de pared
Seguimiento integral y recopilación de datos
Ejemplos de uso en la vida real
Industria	Aplicación
Fabricación	Programación de máquinas, líneas de producción, gestión de inventario
Atención sanitaria	Simulación de salas de urgencias, flujo de pacientes, asignación de personal
Telecomunicaciones	Tráfico de red, enrutamiento de paquetes, asignación de ancho de banda
Transporte	Flujo de tráfico, logística, rutas de vehículos
Operaciones de servicio	Centros de llamadas, caja minorista, programación de citas
Sistemas informáticos	Programación de CPU, gestión de memoria, operaciones de E/S
Alternativas

Si se necesita una herramienta similar a SimPy, la mejor alternativa en Python puro es Salabim: es gratuita, corre completamente en Python y viene con animaciones y gráficos integrados. Para una visión más amplia existen herramientas basadas en R, o herramientas visuales de "arrastrar y soltar" como AnyLogic.

Categoría	Herramienta	Descripción
Python puro	Salabim	La coincidencia más cercana a SimPy; a diferencia de este, incluye gráficos 2D/3D integrados y herramientas avanzadas de visualización.
Python puro	Casymda	Cierra la brecha entre software visual y código: permite dibujar el proceso con diagramas BPMN y los convierte en código Python ejecutable.
Lenguaje R	Simmer	Ideal si se conoce R (especialmente tidyverse); es rápida y facilita la limpieza de datos.
Visual / comercial	AnyLogic	Modelos construidos con bloques visuales, con soporte de código (Java y Python) para partes complejas; admite animación 3D.
Visual / comercial	Simio	Herramienta de arrastrar y soltar, destacada en fábricas, cadenas de suministro y hospitales; ideal para principiantes.
Visual / comercial	Simulink (MathWorks)	Buena opción si ya se usa MATLAB; confiable y altamente escalable.
