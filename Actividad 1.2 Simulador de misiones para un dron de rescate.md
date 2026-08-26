# Actividad 1.2: Simulador de misiones para un dron de rescate 🚁

## 1. Datos generales

**Modalidad:** parejas  
**Duración estimada:** 3 horas  
**Herramientas:** Kotlin, IntelliJ IDEA, Git y GitHub  
**Tipo de programa:** aplicación de consola  
**Restricciones:** no crear clases, objetos personalizados, interfaces, arreglos ni listas.

Pueden emplear variables, entrada y salida, condicionales, `when`, funciones, parámetros predeterminados, funciones de una expresión, lambdas, funciones de orden superior y referencias mediante `::`.

## 2. Propósito

Desarrollar colaborativamente un simulador que evalúe si un dron puede realizar una misión de rescate y calcule el tiempo, consumo de batería y nivel de riesgo estimados.

La práctica busca que cada estudiante demuestre que una función puede:

1. Recibir datos y devolver un resultado.
2. Escribirse como una sola expresión cuando su lógica es breve.
3. Guardarse en una variable mediante una lambda.
4. Recibirse como parámetro de otra función.
5. Cambiar el comportamiento de un cálculo sin reescribir toda la función.

## 3. Situación problemática

Un equipo de protección civil utiliza un dron para llevar suministros a una zona aislada. Antes de autorizar el vuelo necesita evaluar **una misión a la vez**.

El programa solicitará:

* Distancia de ida, en kilómetros.
* Peso de la carga, en kilogramos.
* Porcentaje actual de batería.
* Velocidad del viento, en kilómetros por hora.
* Tipo de carga: `medicina`, `alimento` o `equipo`.
* Condición de vuelo: `normal`, `lluvia` o `emergencia`.

No se almacenará un historial: cada ejecución analizará únicamente los datos capturados en ese momento.

## 4. Reglas simplificadas

### Tiempo de vuelo

* El dron recorre 2 kilómetros por minuto.
* La distancia total será ida y regreso.
* Con lluvia, el tiempo aumenta 20 %.
* En emergencia, el tiempo disminuye 10 % por el aumento de velocidad.

### Consumo de batería

* Se consumen 4 puntos porcentuales por cada kilómetro de distancia total.
* Se agregan 2 puntos por cada kilogramo de carga.
* Con lluvia se agregan 10 puntos porcentuales.
* En emergencia se agregan 5 puntos porcentuales.
* La misión debe finalizar con una reserva mínima de 15 %.

### Riesgo

* Viento menor que 20 km/h: `Bajo`.
* Viento entre 20 y 39 km/h: `Medio`.
* Viento de 40 km/h o más: `Alto`.
* Si la carga pesa más de 5 kg, el riesgo aumenta un nivel.
* Con riesgo `Alto`, la misión no se autoriza.

> Estas reglas son didácticas y no representan especificaciones reales de operación aeronáutica.

## 5. Ejemplo de salida

```text
SIMULADOR DE MISIÓN DE RESCATE

Distancia de ida: 4.0 km
Peso de la carga: 2.5 kg
Batería disponible: 75 %
Velocidad del viento: 18 km/h
Tipo de carga: medicina
Condición: normal

RESULTADO DE LA EVALUACIÓN
Distancia total: 8.0 km
Tiempo estimado: 4.0 minutos
Consumo estimado: 37.0 %
Batería al regresar: 38.0 %
Nivel de riesgo: Bajo
Decisión: MISIÓN AUTORIZADA
```

El programa rechazará datos negativos, batería fuera del intervalo de 0 a 100 y opciones de texto no reconocidas.

---

# Desarrollo de la práctica

## Fase 1. Planeación antes de codificar

Cada estudiante creará en su rama uno de estos archivos:

```text
planeacion-estudiante-a.md
planeacion-estudiante-b.md
```

Antes de implementar cada función deberá indicar:

1. Datos de entrada.
2. Resultado o efecto esperado.
3. Pseudocódigo.
4. Dos casos de prueba, incluido un caso límite.

La planeación tendrá un commit propio y aparecerá en el historial **antes** del código correspondiente.

## Fase 2. Repositorio y ramas

El estudiante A creará el proyecto `DronRescateKotlin`, el repositorio `dron-rescate-kotlin`, el `.gitignore` y un `Main.kt` mínimo. Después hará `push` y agregará al estudiante B.

El estudiante B aceptará la invitación, clonará el repositorio desde IntelliJ IDEA y ejecutará el programa.

Tras hacer `pull` desde `main`, crearán sus ramas:

| Integrante   | Rama               | Responsabilidad inicial              |
| ------------ | ------------------ | ------------------------------------ |
| Estudiante A | `calculos-vuelo`   | Distancia, tiempo y ajustes de vuelo |
| Estudiante B | `seguridad-mision` | Batería, riesgo y autorización       |

## Fase 3. Estudiante A: cálculos de vuelo

### 3.1 Funciones de una sola expresión

```kotlin
fun calcularDistanciaTotal(distanciaIda: Double): Double = TODO()

fun calcularTiempoBase(distanciaTotal: Double): Double = TODO()
```

No deberán contener llaves ni `return` explícito.

### 3.2 Lambdas en variables

```kotlin
val aumentarVeintePorciento: (Double) -> Double = { valor -> TODO() }

val disminuirDiezPorciento: (Double) -> Double = { valor -> TODO() }
```

### 3.3 Función de orden superior

```kotlin
fun aplicarAjuste(
    valorBase: Double,
    ajuste: (Double) -> Double
): Double
```

Esta función ejecutará la función recibida en `ajuste`. No deberá decidir qué porcentaje aumentar o disminuir.

Se probarán las dos formas de pasar una lambda:

```kotlin
val tiempoConLluvia = aplicarAjuste(tiempoBase, aumentarVeintePorciento)

val tiempoEmergencia = aplicarAjuste(tiempoBase) { tiempo ->
    // completar expresión
}
```

### 3.4 Selección del ajuste

```kotlin
fun calcularTiempoFinal(
    tiempoBase: Double,
    condicion: String,
    ajusteLluvia: (Double) -> Double,
    ajusteEmergencia: (Double) -> Double
): Double
```

Usará `when`: en condición normal devolverá el tiempo base; con lluvia aplicará `ajusteLluvia`; en emergencia aplicará `ajusteEmergencia`.

### Commits mínimos del estudiante A

```text
Documenta planeación de cálculos de vuelo
Agrega funciones compactas de distancia y tiempo
Agrega lambdas y ajuste de orden superior
```

## Fase 4. Estudiante B: seguridad de la misión

### 4.1 Función con parámetro predeterminado

```kotlin
fun calcularConsumoBateria(
    distanciaTotal: Double,
    pesoCarga: Double,
    consumoExtra: Double = 0.0
): Double
```

Se llamará al menos una vez utilizando argumentos con nombre:

```kotlin
calcularConsumoBateria(
    distanciaTotal = distancia,
    pesoCarga = peso,
    consumoExtra = 10.0
)
```

### 4.2 Funciones de una sola expresión

```kotlin
fun calcularBateriaFinal(
    bateriaInicial: Double,
    consumo: Double
): Double = TODO()

fun tieneReservaSuficiente(
    bateriaFinal: Double,
    reservaMinima: Double = 15.0
): Boolean = TODO()
```

### 4.3 Lambda de clasificación

```kotlin
val clasificarViento: (Double) -> String = { velocidad ->
    // devolver Bajo, Medio o Alto
}
```

### 4.4 Función de orden superior

```kotlin
fun evaluarRiesgo(
    velocidadViento: Double,
    pesoCarga: Double,
    clasificador: (Double) -> String
): String
```

Usará el clasificador recibido y, si la carga supera 5 kg, aumentará el riesgo: `Bajo` a `Medio`, `Medio` a `Alto` y `Alto` permanecerá igual.

### Commits mínimos del estudiante B

```text
Documenta planeación de seguridad de misión
Agrega cálculo de consumo y reserva de batería
Agrega lambda y evaluación de riesgo
```

## Fase 5. Pull requests y revisión cruzada

Cada estudiante abrirá un pull request de su rama hacia `main`. La descripción incluirá funciones, conceptos de Kotlin, casos de prueba y un aspecto específico que desea que revise su compañero.

El compañero dejará al menos dos comentarios:

1. Uno sobre funcionamiento.
2. Uno sobre claridad o uso de funciones.

Ejemplos:

```text
¿Qué ocurre si la batería calculada al final es negativa?
```

```text
¿Esta lógica breve podría escribirse como función de una sola expresión?
```

```text
¿La función de orden superior realmente utiliza la función recibida?
```

Cada autor atenderá una observación mediante un commit independiente antes de la aprobación y el `merge`.

## Fase 6. Integración y referencia de función

Después del primer `merge`, el otro estudiante actualizará `main` mediante `pull`, integrará `main` en su rama y ejecutará el código completo.

La pareja implementará:

```kotlin
fun autorizarMisionPorSeguridad(riesgo: String): Boolean = TODO()

fun emitirDecision(
    bateriaSuficiente: Boolean,
    riesgo: String,
    criterioSeguridad: (String) -> Boolean
): String
```

La llamada pasará una referencia de función:

```kotlin
val decision = emitirDecision(
    bateriaSuficiente,
    riesgo,
    ::autorizarMisionPorSeguridad
)
```

La misión se autorizará solamente cuando exista reserva suficiente y el criterio de seguridad acepte el riesgo.

## Fase 7. Integración en `main()`

`main()` deberá:

1. Solicitar y validar los seis datos.
2. Calcular distancia y tiempo.
3. Seleccionar el consumo adicional según la condición.
4. Calcular la batería final.
5. Evaluar el riesgo mediante la lambda.
6. Obtener la decisión mediante `emitirDecision()`.
7. Mostrar el reporte completo.

`main()` coordinará el programa, pero no contendrá directamente las fórmulas de cálculo.

## Fase 8. Pruebas obligatorias

La pareja agregará `ejecutarPruebas()` o un archivo `Pruebas.kt`. No se requiere todavía una biblioteca de pruebas.

| Caso                                    | Resultado esperado       |
| --------------------------------------- | ------------------------ |
| Distancia de ida de 5 km                | Distancia total de 10 km |
| Tiempo base de 10 min con lluvia        | Tiempo final de 12 min   |
| Tiempo base de 10 min en emergencia     | Tiempo final de 9 min    |
| Batería final de 15 %                   | Reserva suficiente       |
| Batería final menor que 15 %            | Reserva insuficiente     |
| Viento de 19 km/h y carga ligera        | Riesgo `Bajo`            |
| Viento de 25 km/h y carga mayor de 5 kg | Riesgo `Alto`            |
| Riesgo `Alto` con batería suficiente    | Misión no autorizada     |
| Riesgo `Bajo` con batería insuficiente  | Misión no autorizada     |

Cada integrante agregará dos casos, incluyendo una entrada no válida.

---

# Entregables

1. Enlace al repositorio de GitHub.
2. Programa ejecutable en `main`.
3. Dos archivos de planeación y pseudocódigo.
4. Al menos ocho commits significativos.
5. Una rama y un pull request por estudiante.
6. Comentarios de revisión realizados por ambos.
7. Correcciones derivadas de la revisión.
8. Pruebas ejecutadas y sus resultados.
9. `README.md` con integrantes, responsabilidades, instrucciones de ejecución, funciones de expresión única, lambdas, funciones de orden superior, uso de `::`, pruebas y conclusiones individuales.

## Evidencia individual en el README

Cada estudiante responderá:

1. ¿Qué diferencia existe entre una función nombrada y una lambda?
2. ¿Qué caracteriza a una función de una sola expresión?
3. ¿Cuál función es de orden superior y por qué?
4. ¿Qué ventaja tuvo pasar el ajuste o criterio como parámetro?
5. ¿Qué diferencia encontró entre pasar una lambda y usar `::autorizarMisionPorSeguridad`?
6. ¿Qué parte desarrolló personalmente?
7. ¿Qué modificó después de la revisión de su compañero?

# Criterios de evaluación

| Criterio                                                    | Porcentaje |
| ----------------------------------------------------------- | ----------:|
| Funcionamiento, validación e integración                    | 20 %       |
| Funciones con parámetros, retorno y valores predeterminados | 15 %       |
| Funciones de una sola expresión                             | 10 %       |
| Declaración y uso de lambdas                                | 15 %       |
| Funciones de orden superior                                 | 20 %       |
| Referencia de función mediante `::`                         | 5 %        |
| Planeación, pseudocódigo y pruebas                          | 5 %        |
| Trabajo colaborativo y revisión en GitHub                   | 10 %       |
| **Total**                                                   | **100 %**  |

## Condición de participación individual

Cada estudiante deberá aparecer en GitHub como autor de su planeación, tres commits funcionales, una rama, un pull request, una corrección, dos comentarios de revisión, una función de expresión única, una lambda y una contribución a una función de orden superior o a su uso.

No se considerará participación suficiente limitarse a cambios de formato, copiar el código del compañero o aparecer solamente en el documento final.

## Adaptación para equipos de tres

El tercer integrante utilizará la rama `pruebas-integracion` y se encargará de validar entradas, implementar pruebas, integrar el reporte final y crear una lambda adicional para la condición `viento-fuerte`. También abrirá su propio pull request y revisará el de otro integrante.

# Recursos

* [Android Developers: Lesson 2 — Functions](https://developer.android.com/courses/pathways/android-development-with-kotlin-2)
* [Kotlin: Functions](https://kotlinlang.org/docs/functions.html)
* [Kotlin: Lambdas and higher-order functions](https://kotlinlang.org/docs/lambdas.html)
* [GitHub: About pull requests](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
