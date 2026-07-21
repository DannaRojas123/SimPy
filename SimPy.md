# SimPy
Los ingenieros industriales y de fabricación están a cargo de muchos procesos en su carrera, e incluso podría llegar a un punto en el que te abrume con la cantidad de cosas que debes controlar. SimPy, una biblioteca de Python, existe desde 2002 para modelar procesos en un formato simple para que los nuevos codificadores aprendan y lo utilicen.

El entorno es lo que permite que comience la simulación porque realiza un seguimiento de todos los procesos que ocurren en el código real. Debido a que puede realizar un seguimiento del tiempo, primero lo crea y le agrega procesos, por lo que una vez que ejecuta el código y se ejecuta la función de entorno, comienza el tiempo y realiza un seguimiento de lo que ocurre con sus procesos, recursos, etc.
Sin embargo, para hacer uso del entorno, tenemos que comprender la función del proceso, que es lo que los entornos rastrean. 

Los procesos varían mucho; sin embargo, todos representan acciones que ocurren a lo largo del tiempo y puedes ejecutar varias a la vez dentro del entorno. Puede utilizar diferentes variables para realizar un seguimiento de las diferentes tareas que ocurren en el entorno, lo que ayuda a simular cómo podría ejecutarse una línea de ensamblaje. Para escribir cómo ocurriría un proceso, primero tenemos que definir el proceso antes de ejecutar el entorno. Esto significa simular cuándo comenzaría el trabajo y cuánto tiempo tomaría. Y después de definir el trabajo, lo ejecutas como un proceso después de definir el entorno.

## Caracteristicas
SimPy es un Marco de simulación de eventos discretos (DES) basado en procesos escrito en Python. Le permite modelar componentes activos del mundo real (como clientes o vehículos) utilizando funciones generadoras de Python.
- Simulación de eventos discretos (DES): la simulación salta de un evento específico al siguiente, en lugar de seguir cada milisegundo de forma continua. Esto permite que los modelos funcionen increíblemente rápido sin desperdiciar energía de la computadora en períodos inactivos.
- Basado en Python: debido a que utiliza Python estándar, puede aprovechar todo el ecosistema de Python. Puede conectar fácilmente bibliotecas comopandas para ingresar datos ymatplotlib graficar resultados.
- Orientado a procesos: en lugar de centrarse en ecuaciones matemáticas globales, escribe componentes activos (como un "cliente" que va a un banco) utilizando funciones generadoras de Python. Simplemente le dices al proceso qué hacer paso a paso y dónde esperar.
- Gestión de recursos compartidos: SimPy proporciona herramientas integradas para gestionar las limitaciones del mundo real. Incluye:Recursos: Para artículos con capacidad limitada (por ejemplo, 2 cajeros, 1 lugar de estacionamiento).Contenedores: Para cantidades continuas (por ejemplo, combustible en un tanque o agua en una tubería).Tiendas: Para inventario de artículos discretos (por ejemplo, repuestos de automóviles en un estante).
- Ejecución de tiempo flexible: puede ejecutar simulaciones de tres maneras:Lo más rápido posible: ejecuta todo el modelo en segundos. Tiempo real: sincronizado con tu reloj real.Paso a paso: Pausas para verificación y depuración manual.
- Sin GUI incorporada: SimPy es puramente una biblioteca de codificación. No tiene animación incorporada ni interfaz de usuario, lo que significa que usted es responsable de codificar la salida de datos y las visualizaciones.
## ¿Dónde se utiliza?
1. Modelado de procesos utilizando funciones generadoras de Python
2. Gestión de recursos compartidos (servidores, contenedores, tiendas)
3. Programación y sincronización basadas en eventos
4. Simulaciones en tiempo real sincronizadas con el tiempo del reloj de pared
5. Seguimiento integral y recopilación de datos

#### Ejemplos de uso en la vida real: 
- Fabricación: Programación de máquinas, líneas de producción, gestión de inventario
- Atención sanitaria: simulación de salas de urgencias, flujo de pacientes, asignación de personal
- Telecomunicaciones: tráfico de red, enrutamiento de paquetes, asignación de ancho de banda
- Transporte: Flujo de tráfico, logística, rutas de vehículos
- Operaciones de servicio: Centros de llamadas, caja minorista, programación de citas
- Sistemas informáticos: programación de CPU, gestión de memoria, operaciones de E/S

## Recursos que se pueden utilizar
<img width="877" height="320" alt="image" src="https://github.com/user-attachments/assets/7bc46286-8d74-41b2-8555-c0ff136c0915" />

## Alternativas
Si necesitas una herramienta como SimPy, la mejor alternativa pura a Python es Salabim. Salabim es gratuito, se ejecuta completamente en Python y es fantástico porque incluye animaciones y gráficos integrados. Para una visión más amplia, considere herramientas basadas en R como Herramientas visuales o de cocción lenta como AnyLogic.

Las mejores alternativas dependen de tus necesidades exactas:
1. Las mejores alternativas a Python (código puro)
   - Salabim: Esta es la coincidencia más cercana a SimPy. Le permite crear simulaciones de eventos discretos en Python. A diferencia de       SimPy, viene con gráficos 2D/3D integrados y herramientas de gráficos avanzadas para ver cómo se ejecuta su simulación.
   - Casymda: una herramienta divertida que cierra la brecha entre el software visual y el código. Le permite dibujar su proceso               visualmente (usando diagramas BPMN) y convierte esos dibujos en código Python ejecutable.
2. Ideal para científicos de datos (lenguaje R)
   - Simmer: si sabes cómo utilizar el lenguaje de programación R (especialmente eltidyverse ), simmer es la opción perfecta. Es muy           rápido, funciona bien con canales de datos y facilita la limpieza de datos.
3. Ideal para software comercial y visual (arrastrar y soltar)Si está cansado de escribir código y desea crear modelos visualmente, puede consultar estos paquetes de software de primer nivel:
   - AnyLogic: una herramienta resistente. Construyes modelos usando bloques visuales, pero aún puedes usar código (Java y Python) para        partes complicadas. Es muy visual y admite animación 3D.
   - Simio: una famosa herramienta de arrastrar y soltar que se destaca en fábricas de modelos, cadenas de suministro y hospitales. Es         ideal para principiantes pero maneja bien sistemas complejos.
   - Simulink (MathWorks): una gran opción si ya usas MATLAB. Es confiable y altamente escalable.
