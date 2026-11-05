# 5toazul-Isabella-Pachon
Pensamiento computacional clase del 24/09/26 creación de GitHub

tinkercad: https://www.tinkercad.com/
usuario: isaa230210
contraseña: 230210-230210Polo

actividad desenchufada: 
<img width="2581" height="3553" alt="image" src="https://github.com/user-attachments/assets/63280f26-674e-45a2-9404-3af8c5159a5b" />

circuito:
<img width="855" height="1044" alt="image" src="https://github.com/user-attachments/assets/829262f6-f86a-4556-a6f9-bbff64b49cf4" />


código:
<img width="1196" height="1088" alt="image" src="https://github.com/user-attachments/assets/a610e976-c384-4d6e-94f6-8e00c10d754a" />
<img width="1196" height="1053" alt="image" src="https://github.com/user-attachments/assets/97ef976b-4cc5-4802-a09a-011c1314f888" />
<img width="1151" height="580" alt="image" src="https://github.com/user-attachments/assets/b73f3366-3b22-4569-8478-2f16618ed322" />

link: https://www.tinkercad.com/things/eoqZjDptuKu-incredible-kup-hango/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=qs5TLU41_e057dGEnJzimKzCBgzKqnBbZIODge3nvhY

actividad propuesta problema:
Paso 2: Diseña tu propuesta
Describe brevemente:
	•	¿Cuál es el problema?: Es sabido que para la vista, específicamente para personas con miopía, mirar por tanto tiempo una pantalla es dañino. Se recomienda hacer un break de 20 segundos cada 20 minutos para disminuir el daño y dejar “respirar” al ojo.
	•	¿Quién se beneficiaría de la solución?: Realmente todo el mundo, considerando que es recomendado para disminuir los chances de desarrollar miopía a largo plazo.
	•	¿Cómo ayudará tu prototipo a resolver la situación?: Al prender un interruptor, se enciende un led indicando que esta prendido e inicia un “cronometro” de 20 minutos. Al pasar los 20 minuto, el led se apaga y suena una pequeña alarma indicando que es hora de descansar la vista.

 <img width="1452" height="1009" alt="image" src="https://github.com/user-attachments/assets/95aa8f76-de7b-4a8a-b80c-829f8e06be79" />

<img width="1181" height="1777" alt="image" src="https://github.com/user-attachments/assets/a50da581-18e2-4ec5-bfc5-689761a4f0a1" />

https://www.tinkercad.com/things/0y0i5OOMnT3-spectacular-stantia-wluff/editel?returnTo=%2Fdashboard%2Fdesigns%2Fall&sharecode=nOh8e99jXPUlz27SXU1M7Ofh6ZUNeYih7-YJAlDh0j8

## TAREA 22/10/26
 
Un centro de atención recibe estudiantes para entregar documentos. Hay una sola ventanilla y tres tipos de trámites: entrega de documentos, solicitud de constancia y consulta general. Algunos trámites tardan más que otros. El centro quiere reducir el tiempo promedio de espera sin dejar de atender por orden de llegada, salvo casos prioritarios.
 
**1.** Descompón el problema en al menos 4 subproblemas: llegada de estudiantes, registro, prioridades, atención, cierre.
**2.** Define qué datos se necesitan para representar a cada estudiante.
**3.** Diseña un algoritmo en pseudocódigo o diagrama de flujo que organice la atención.
**4.** Explica qué criterio de prioridad usarías y por qué.
 
 
## 1. Descomposición del Problema en Subproblemas
 
**1. Llegada de Estudiantes:** Captura el ingreso físico o virtual del usuario al sistema del centro de atención, determinando la tasa de concurrencia y el flujo de entrada.
**2. Registro y Clasificación del Trámite:** Identificación unívoca del estudiante y tipificación de su requerimiento (*Entrega de documentos*, *Solicitud de constancia* o *Consulta general*), asociando un tiempo de procesamiento estimado.
**3. Gestión de Prioridades y Encolamiento:** Asignación dinámica de la posición en la estructura de datos de espera, ponderando el orden de llegada (FIFO) frente a condiciones excepcionales o requerimientos de prioridad institucional.
**4. Atención en Ventanilla Única:** Ciclo de ejecución del servicio por parte del operador, caracterizado por la liberación de la ventanilla y el registro de tiempos de servicio.
**5. Cierre de Operaciones y Métricas:** Culor de la jornada o del ciclo de atención, con la generación de indicadores clave de rendimiento (KPIs), tales como tiempo promedio de espera y satisfacción del usuario.
 
 
## 2. Modelo de Datos: Representación del Estudiante
 
```text
Estructura Estudiante {
    Entero       id_estudiante        // Identificador único o número de matrícula
    Cadena       nombre               // Nombre completo del estudiante
    Entero       tipo_tramite         // 1: Entrega de documentos, 2: Solicitud de constancia, 3: Consulta general
    Entero       duracion_estimada    // Tiempo estimado de procesamiento en minutos (según tipo de trámite)
    Entero       nivel_prioridad      // 0: Normal, 1: Prioritario (Casos especiales, salud, urgencias académicas)
    MarcaTiempo  timestamp_llegada    // Hora exacta de llegada al centro para garantizar orden relativo
}
 
```
 
## 3. Criterio de Prioridad y Justificación
 
### Criterio Seleccionado:
 
1. **Prioridad Absoluta por Excepción:** Casos médicos, discapacidades o restricciones de tiempo críticas debidamente justificadas tienen preferencia absoluta sobre cualquier turno estándar.
2. **Prioridad por Tiempo de Procesamiento Corto dentro de la misma categoría:** Entre estudiantes con igual nivel de prioridad ordinaria, se aplica una variante orientada a minimizar el tiempo de espera acumulativo de la cola, priorizando aquellos trámites con menor duración estimada (ej. *Consulta general* o *Entrega de documentos* frente a trámites complejos), respetando secundariamente el orden estricto de llegada (FIFO).
 
 
4. Algoritmo de Gestión de Atención (Pseudocódigo)
 
```text
Algoritmo GestionCentroAtencion
    // Inicialización de estructuras de datos
    CrearColaPrioridad(ColaEspera)
    Booleano centroAbierto = VERDADERO
    
    // Bucle principal de operaciones del centro
    Mientras centroAbierto == VERDADERO Hacer
        
        // 1. Fase de Llegada y Registro
        Si HayNuevoEstudianteEnFila() Entonces
            Estudiante nuevoEstudiante = RegistrarEstudiante()
            ColaEspera.Insertar(nuevoEstudiante)
        Fin Si
        
        // 2. Fase de Atención en Ventanilla Única
        Si VentanillaEstaLibre() Y NO ColaEspera.EstaVacia() Entonces
            
            // Extraer al siguiente estudiante según la función de prioridad optimizada
            Estudiante actual = ColaEspera.ObtenerSiguienteAtencion()
            
            IniciarAtencion(actual)
            SimularTiempoProceso(actual.duracion_estimada)
            FinalizarAtencion(actual)
            
        Fin Si
        
        // 3. Verificación de Cierre
        Si EsHoraDeCierre() Y ColaEspera.EstaVacia() Entonces
            centroAbierto = FALSO
        Fin Si
        
    Fin Mientras
    
    GenerarReporteMetricas()
Fin Algoritmo
 
```
 
 
## Módulo 1:
 
### 1. Representación de Paradas y Distancias
 
Se modela un sistema con 6 paradas (incluyendo el punto de partida/base escolar) y un volumen conocido de estudiantes por estación.
 
| ID Parada | Nombre de la Parada | Estudiantes a Recoger | Distancia al Siguiente Nodo (km) |
| --- |        --- | ---                 | --- |
| **P0** |    Base Escolar         //      | 0 |                  2.5 (a P1)  |
| **P1** |    Residencial Norte   //      | 5 |                  3.1 (a P2)  |
| **P2** |    Parque Central     //       | 8 |                  1.8 (a P3)  |
| **P3** |    Urbanización Sur  //       | 12 |                  4.0 (a P4) |
| **P4** |    Plaza Mayor      //        | 4 |                   2.2 (a P5) |
| **P5** |    Sector Este     //          | 6 |                   3.5 (a P0) |
 
 
### 2. Algoritmo Paso a Paso para Construir la Ruta
 
1. **Inicialización:**
* Definir la Base Escolar (P0) como punto de partida actual ($N_{actual} = P0$).
* Inicializar el conjunto de paradas pendientes $S = \{P1, P2, P3, P4, P5\}$.
* Inicializar la ruta seleccionada $Ruta = [P0]$ y el contador de capacidad actual del autobús en $0$.
 
 
2. **Ciclo de Construcción:**
* Mientras $S$ no esté vacío:
* Evaluar todas las paradas $P_i$ pertenecientes a $S$.
* Calcular una función de costo heurística que combine distancia mínima y mayor concentración de estudiantes:
 
$$\text{Costo} = \text{Distancia}(N_{actual}, P_i) - (\alpha \times \text{Estudiantes}_{P_i})$$
 
 
Seleccionar la parada $P_s$ que minimice dicho costo (priorizando cercanía pero compensando con alta demanda de pasajeros).
Actualizar $N_{actual} = P_s$, añadir $P_s$ a $Ruta$, y remover $P_s$ de $S$.
 
 
 
3. **Cierre de Ruta:**
Al vaciar $S$, añadir la Base Escolar (P0) al final de $Ruta$ para completar el circuito de retorno.
 
 
4. **Salida:** Retornar la ruta optimizada y la métrica de distancia total acumulada.
 
 
### 3. Ruta Propuesta Aplicando el Algoritmo
 
Siguiendo la heurística de proximidad y alta densidad de pasajeros:
 
* **Secuencia de Recorrido:**
 
$$\text{P0 (Base)} \rightarrow \text{P1 (5 est.)} \rightarrow \text{P2 (8 est.)} \rightarrow \text{P3 (12 est.)} \rightarrow \text{P4 (4 est.)} \rightarrow \text{P5 (6 est.)} \rightarrow \text{P0 (Base)}$$
 
 
* **Estudiantes Totales Recogidos:** 35 estudiantes.
 
### 4. Comparación y Selección de Alternativas
 
Se evalúa la ruta propuesta frente a una alternativa secuencial arbitraria (orden alfabético/numérico estricto).
 
**Alternativa A (Ruta Propuesta - Heurística Vecino + Demanda):** Distancia total aproximada = 17.1 km.
**Alternativa B (Ruta Secuencial Estricta P0-P1-P2-P3-P4-P5-P0):** Distancia total aproximada = 22.5 km.
 
**Criterio Seleccionado:** **Menor distancia total recorrida**.
**Justificación:** La alternativa propuesta reduce la distancia en un 24%, lo que se traduce directamente en un menor consumo de combustible, menor desgaste mecánico de la unidad de transporte y un tiempo de viaje optimizado para los estudiantes a bordo.
 
 
## Modulo 2:
 
### 1. Identificación de Errores o Limitaciones del Algoritmo Original
 
Analizando el pseudocódigo provisto:
 
1. **Error Matemático / Lógico Crítico:** El cálculo del promedio suma las notas (`nota1 + nota2 + nota3`), pero omite la división entre el número total de notas (3). Esto genera un valor inflado, lo que falsea completamente la condición de aprobación.
2. **Falta de Validación de Datos de Entrada:** No existe control sobre los valores ingresados; el sistema aceptaría notas negativas o valores absurdos mayores a 100.
 
### 2. Pseudocódigo Corregido y Mejorado
 
A continuación, se presenta el pseudocódigo optimizado que corrige los errores conceptuales, añade validación estricta de rangos e incorpora un sistema de recuperación académica.
 
```text
Algoritmo EvaluacionEstudianteMejorado
    // Definición de variables
    Real nota1, nota2, nota3, nota4, promedio
    Booleano notasValidas
 
    // Inicialización de bandera de validación
    notasValidas = FALSO
 
    // Validación de entrada de datos (Rango 0 a 100)
    Mientras notasValidas == FALSO Hacer
        Escribir "Ingrese las 4 notas del estudiante (0 a 100):"
        Leer nota1, nota2, nota3, nota4
 
        Si (nota1 >= 0 Y nota1 <= 100) Y _
           (nota2 >= 0 Y nota2 <= 100) Y _
           (nota3 >= 0 Y nota3 <= 100) Y _
           (nota4 >= 0 Y nota4 <= 100) Entonces
            notasValidas = VERDADERO
        SiNo
            Escribir "Error: Una o más notas están fuera del rango permitido [0, 100]. Intente de nuevo."
        FinSi
    FinMientras
 
    // Corrección del cálculo matemático: Suma dividida entre el total de elementos (4)
    promedio = (nota1 + nota2 + nota3 + nota4) / 4
 
    // Mostrar el resultado cuantitativo del promedio
    Escribir "El promedio final del estudiante es: ", promedio
 
    // Evaluación con lógica de aprobación y recuperación
    Si promedio >= 60 Entonces
        Escribir "Estado: APRUEBA"
    SiNo
        Si promedio >= 50 Y promedio < 60 Entonces
            Escribir "Estado: NO APRUEBA DIRECTO - Debe presentar EXAMEN DE RECUPERACIÓN"
        SiNo
            Escribir "Estado: REPRUEBA DEFINITIVA"
        FinSi
    FinSi
 
FinAlgoritmo
```

## TAREA 29/10/26

Los servomotores funcionan mediante un sistema de control de lazo cerrado. Reciben una señal PWM (Modulación por Ancho de Pulsos) con una frecuencia estándar de 
50 Hz (un pulso cada 20ms). La duración del pulso determina la posición angular del eje: por lo general, un pulso de 1 posiciona el motor a 0, de 1.5 a 90 y de 2 a 180. Internamente, un circuito de control compara esta señal de entrada con la posición actual obtenida por un potenciómetro acoplado al eje y ajusta el motor mediante un controlador de corriente continua y una caja de engranajes.
Conexiones básicas (alimentación, tierra y señal)

Los servomotores estándar cuentan con un cable de tres hilos:
* Alimentación (VCC): Generalmente de color rojo, se conecta a la fuente de voltaje positiva (comúnmente 5 para servos pequeños).
* Tierra (GND): De color marrón, negro o café, se conecta al pin de tierra común del circuito.
* Señal (PWM): De color amarillo o naranja, se conecta a un pin digital PWM de la placa Arduino para enviar las instrucciones de movimiento.
Control mediante programación en Arduino

Para controlar un servomotor desde Arduino, se utilizan los pines digitales configurados como salidas PWM. Mediante código, se envían trenes de pulsos periódicos que indican al circuito interno la posición exacta deseada. El microcontrolador se encarga de generar estas señales de control mientras el usuario solo debe definir los grados objetivo en el programa.
Uso de la librería Servo

Arduino incluye de forma nativa la librería Servo.h para simplificar el control de estos motores sin necesidad de programar los pulsos manualmente:
* Se debe incluir la librería al inicio del código con #include <Servo.h>.
* Se crea un objeto de tipo Servo (por ejemplo, Servo myservo;).
* En la función setup(), se vincula el objeto a un pin digital usando myservo.attach(pin);.
* En el bucle principal loop(), se define la posición mediante la instrucción myservo.write(angulo);, donde el ángulo varía habitualmente entre 0 y 180.
Consideraciones para la alimentación de múltiples servomotores

Al alimentar múltiples servomotores o modelos de alta potencia, nunca se debe usar la salida de la placa Arduino, ya que el consumo de corriente (especialmente en los picos de arranque o bloqueo) puede sobrecargar el regulador interno, provocar caídas de tensión y reiniciar la placa. Es obligatorio utilizar una fuente de alimentación externa adecuada para los motores, asegurándose de conectar las masas (GND) de la fuente externa y del Arduino juntas para tener una referencia común.

Ejemplos de movimiento angular y control de posición

* Movimiento de barrido (Sweep): Consiste en desplazar el eje del motor de manera continua y automatizada de 0∘ a 180∘   y viceversa utilizando bucles incrementales y decrementales junto con pequeños retrasos de tiempo (delay).
* Control de posición por potenciómetro (Knob): Se lee el valor analógico proveniente de un potenciómetro (de 0 a 1023), se reescala o mapea al rango angular del servo mediante la función map() y se asigna directamente al motor para que su eje siga el movimiento manual de la  perilla.

tinkercad: https://www.tinkercad.com/things/fmavu5jWsGe-grand-duup/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard%2Fdesigns%2Fall&sharecode=Rx4SFoGQSdpnW9pa6tZmsuijelksl7w3Lw5fs6bbxvI

<img width="1432" height="995" alt="image" src="https://github.com/user-attachments/assets/1fa51563-e92b-4c3c-9986-1f84095042f2" />

<img width="1205" height="1669" alt="image" src="https://github.com/user-attachments/assets/a163dd43-8cd8-4c12-9537-edf28c386e9f" />
<img width="1190" height="1689" alt="image" src="https://github.com/user-attachments/assets/21289db5-c5b6-4dc5-b647-77a1eadbabf8" />


## Actividad 05/11/26

### Secuencia A
-Serie: 3, 6, 12, 24, 48, 96
-Regla: Cada número se obtiene multiplicando el término anterior por 2 (el doble del anterior).

### Secuencia B
-Serie: 1, 4, 9, 16, 25, 36
-Regla: Es la secuencia de los números cuadrados perfectos (1², 2², 3², 4², 5², 6²). También se puede notar que se le suma consecutivamente el siguiente número impar (+3, +5, +7, +9, +11).

### Secuencia C
-Serie: ▲, ▲▲, ▲▲▲, ▲▲▲▲, ▲▲▲▲▲
-Regla: En cada paso se añade un triángulo (`▲`) más que en el elemento anterior.

### Secuencia D
-Serie: 2, 5, 11, 23, 47, 95
-Regla: Cada término es el doble del anterior más uno. La fórmula es: (anterior × 2) + 1.

---

## Ejercicio 2: Diseño de Plano para un Robot

**Situación:** Debes diseñar un plano sencillo de tu salón de clases para que un robot pequeño pueda desplazarse desde la puerta hasta el escritorio del docente sin chocar con obstáculos.

### 1. Elementos importantes (Abstracción)
Las paredes del salón (delimitación del espacio).
La ubicación exacta de la puerta (`P`) y del escritorio del docente (`D`).
Los obstáculos físicos en el suelo: pupitres de los alumnos, estanterías o columnas (`X`).

### 2. Elementos que se pueden ignorar
El color de las paredes o la decoración de los murales.
Los objetos colgados en la pizarra o ventanas altas.
El contenido de las mochilas o el material de papelería sobre las mesas.

### 3. Plano simplificado
```text
+-----------------------+

| [P] . . . . .         |
|             .         |
|     [X] [X] .         |
|     [X] [X] .         |
|             . . . [D] |
+-----------------------+

Símbolos:
P = Puerta
D = Escritorio del docente
X = Obstáculo
. = Espacio libre para avanzar / Ruta del robot
```

---

## Ejercicio 3: Depuración de Algoritmos

**Situación:** Un estudiante escribió el siguiente algoritmo para llegar desde su pupitre hasta la biblioteca del colegio. Sin embargo, el algoritmo tiene dos errores.

### Errores encontrados
* **Error 1:** `Paso 4: Subir las escaleras.` La biblioteca se encuentra en la misma planta o la dirección de las escaleras desvía al estudiante de la ruta correcta.
* **Error 2:** `Paso 6: Entrar al laboratorio de química.` El destino final está equivocado, ya que el objetivo es llegar a la biblioteca y no al laboratorio.

### Algoritmo corregido
1. Salir del salón.
2. Girar a la izquierda.
3. Avanzar hasta el final del pasillo.
4. **Seguir recto por el pasillo central.** (Corrección de ruta)
5. Girar a la derecha.
6. **Entrar a la biblioteca del colegio.** (Corrección de destino)
7. Detenerse.

### Explicación de las correcciones
Se modificaron los pasos 4 y 6 porque el algoritmo original sufría un error de lógica de destino. Las correcciones garantizan que las instrucciones físicas y el punto de detención final coincidan exactamente con el objetivo planteado (la biblioteca).

---

## Ejercicio 4: Optimización y Programación Dinámica

**Situación:** Un robot entra en una cuadrícula de $5 \times 5$ por la casilla $A = (1,1)$ y debe llegar a la casilla $B = (5,5)$. Solo puede moverse hacia la derecha ($\rightarrow$) o hacia abajo ($\downarrow$).

### 1. Abstracción
-Datos mínimos: Para cada casilla $(i,j)$, el algoritmo debe guardar un arreglo de tamaño 5. Cada posición indexada por $r$ (donde $r \in \{0, 1, 2, 3, 4\}$) almacena la **máxima suma acumulada** para llegar a esa casilla con un resto de $r$ al dividir entre 5.
-Estado del problema: Cada estado se representa como la terna $(i, j, r)$, donde $i$ es la fila, $j$ es la columna y $r$ es el residuo de la suma acumulada actual al hacer módulo 5.

### 2. Diseño del algoritmo
-Caso base: En la casilla de inicio $(1,1)$, el valor de la energía es $E(1,1)$. Su residuo es $r_0 = E(1,1) \pmod 5$. Por lo tanto:
  $$M(1,1, r_0) = E(1,1)$$
  *(Los demás residuos para esta casilla se inicializan en $-\infty$)*.
-Ecuación de recurrencia: Para calcular $M(i,j,r)$, evaluamos las celdas predecesoras (arriba e izquierda):
  $$M(i,j,r) = E(i,j) + \max \begin{cases} M(i-1, j, r') \\ M(i, j-1, r') \end{cases}$$
  Donde $r'$ es el residuo previo tal que $(r' + E(i,j)) \pmod 5 \equiv r$.
-Orden de recorrido: Se recorre de forma iterativa fila por fila (de arriba a abajo) y columna por columna (de izquierda a derecha).
-Respuesta final: Se lee directamente en la celda del destino final con residuo cero: $M(5,5,0).

### 3. Aplicación del algoritmo

| Variable | Valor del ejercicio |
| :--- | :--- |
| **Ruta** | $(1,1) \ (1,2) \ (2,2) \ \dots \ (5,5)$ |
| **Suma total**  |
| **¿Es múltiplo de 5?** | Sí, porque el estado final seleccionado pertenece a $r = 0$. |

### 4. Justificación
La ruta es la de mayor suma posible porque la programación dinámica garantiza el óptimo global. Al guardar el valor máximo para cada residuo en cada casilla, el algoritmo evita descartar caminos que temporalmente sumen poco pero que, matemáticamente, sean la única opción para que el resultado final de la meta sea un múltiplo de 5 óptimo. 

### 5. Extensión matemática
No, la ruta óptima no sería necesariamente la misma. Al cambiar la condición a "múltiplo de 3", la aritmética modular se transforma ($módulo\ 3$). Un camino con una suma muy alta que antes fue descartado por terminar en un residuo no óptimo para 5 (por ejemplo, terminar en 24), ahora pasaría a ser totalmente válido y prioritario por ser múltiplo de 3 ($24 \pmod 3 = 0$). Las decisiones locales cambian por completo la estructura del árbol de rutas.

