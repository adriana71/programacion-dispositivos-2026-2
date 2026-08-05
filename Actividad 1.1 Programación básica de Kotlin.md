# Práctica: gestor de gastos de un estudiante

## 1. Datos generales

**Modalidad:** parejas
**Duración estimada:** 3 horas
**Herramientas:** Kotlin, IntelliJ IDEA, Git y GitHub
**Tipo de programa:** aplicación de consola
**Restricción:** no crear clases, objetos personalizados ni interfaces.

Pueden emplear:

* Variables y constantes.
* Funciones.
* Condicionales.
* `when`.
* Ciclos.
* Arreglos o listas.
* Entrada y salida de datos.
* Funciones estándar de Kotlin.

## 2. Propósito

Desarrollar colaborativamente un programa que permita registrar y consultar los gastos semanales de un estudiante, utilizando GitHub como repositorio compartido.

Al finalizar, cada integrante deberá demostrar que sabe:

1. Vincular IntelliJ IDEA con GitHub.
2. Clonar un repositorio.
3. Crear y cambiar de rama.
4. Identificar archivos modificados.
5. Crear commits descriptivos.
6. Enviar cambios mediante `push`.
7. Descargar e integrar cambios mediante `pull`.
8. Crear y revisar un pull request.
9. Fusionar ramas mediante `merge`.
10. Resolver un conflicto sencillo.

## 3. Funcionamiento del programa

El sistema presentará este menú:

```text
GESTOR SEMANAL DE GASTOS

1. Registrar gasto
2. Mostrar todos los gastos
3. Calcular gasto total
4. Mostrar gasto mayor
5. Mostrar gastos por categoría
6. Mostrar resumen semanal
7. Salir

Seleccione una opción:
```

Cada gasto tendrá:

* Concepto.
* Categoría.
* Monto.

Las categorías permitidas serán:

1. Alimentos.
2. Transporte.
3. Materiales escolares.
4. Entretenimiento.
5. Otros.

Como todavía no se utilizarán clases, los datos se almacenarán en tres listas relacionadas:

```kotlin
val conceptos = mutableListOf<String>()
val categorias = mutableListOf<String>()
val montos = mutableListOf<Double>()
```

El elemento de la posición `0` de cada lista corresponde al mismo gasto.

## 4. Organización de la pareja

Cada estudiante tendrá su propia rama:

| Integrante   | Rama              | Responsabilidad inicial           |
| ------------ | ----------------- | --------------------------------- |
| Estudiante A | `registro-gastos` | Registro y presentación de gastos |
| Estudiante B | `analisis-gastos` | Cálculos y consultas              |

Después intercambiarán funciones: cada estudiante revisará e integrará el trabajo del compañero.

---

# Desarrollo de la práctica

## Fase 1. Creación del repositorio

### Actividad del estudiante A

1. Crear en IntelliJ IDEA un proyecto de Kotlin llamado:

```text
GestorGastosKotlin
```

2. Crear un repositorio en GitHub llamado:

```text
gestor-gastos-kotlin
```

3. Vincular el proyecto con GitHub desde IntelliJ IDEA.

Dependiendo de la versión instalada, puede encontrarse en:

```text
Git → GitHub → Share Project on GitHub
```

o:

```text
VCS → Share Project on GitHub
```

4. Agregar un archivo `.gitignore` apropiado para IntelliJ IDEA.

5. Crear el archivo `Main.kt` con el código mínimo:

```kotlin
fun main() {
    println("Gestor semanal de gastos")
}
```

6. Realizar el primer commit:

```text
Inicializa proyecto Kotlin del gestor de gastos
```

7. Ejecutar `push`.

8. Agregar al estudiante B como colaborador del repositorio.

### Actividad del estudiante B

1. Aceptar la invitación de colaboración.
2. Iniciar sesión en GitHub desde IntelliJ IDEA.
3. Clonar el repositorio:

```text
File → New → Project from Version Control
```

4. Ejecutar el programa.
5. Verificar que aparezca:

```text
Gestor semanal de gastos
```

6. Informar al compañero que el proyecto pudo clonarse y ejecutarse.

## Evidencia de la fase

* URL del repositorio.
* Captura del primer commit.
* Captura del proyecto clonado en el equipo del estudiante B.

---

## Fase 2. Creación de ramas

Antes de modificar el código, ambos estudiantes deberán comprobar que se encuentran en `main` y ejecutar un `pull`.

### Estudiante A

Crear la rama:

```text
registro-gastos
```

### Estudiante B

Crear la rama:

```text
analisis-gastos
```

En IntelliJ IDEA pueden utilizar el selector de ramas situado normalmente en la esquina inferior derecha o el menú:

```text
Git → Branches
```

Cada estudiante debe comprobar que está trabajando en su propia rama antes de editar código.

---

# Fase 3. Trabajo del estudiante A

En la rama `registro-gastos`, el estudiante A implementará:

```kotlin
fun registrarGasto(
    conceptos: MutableList<String>,
    categorias: MutableList<String>,
    montos: MutableList<Double>
)
```

La función deberá:

* Solicitar el concepto.
* Mostrar las categorías disponibles.
* Validar la categoría seleccionada.
* Solicitar el monto.
* Rechazar cantidades iguales o menores que cero.
* Agregar los datos a las tres listas.

También implementará:

```kotlin
fun mostrarGastos(
    conceptos: List<String>,
    categorias: List<String>,
    montos: List<Double>
)
```

La salida deberá tener una presentación semejante a esta:

```text
GASTOS REGISTRADOS

1. Comida      | Alimentos  | $85.00
2. Autobús     | Transporte | $22.00
3. Cuaderno    | Materiales | $48.50
```

### Commits obligatorios del estudiante A

Deberá hacer al menos dos commits separados:

```text
Agrega función para registrar gastos
```

```text
Agrega listado de gastos registrados
```

Después ejecutará `push` de la rama `registro-gastos`.

No deberá mezclar ambas funciones en un solo commit.

---

# Fase 4. Trabajo del estudiante B

En la rama `analisis-gastos`, el estudiante B implementará:

```kotlin
fun calcularTotal(montos: List<Double>): Double
```

```kotlin
fun obtenerPosicionGastoMayor(montos: List<Double>): Int
```

```kotlin
fun calcularTotalPorCategoria(
    categorias: List<String>,
    montos: List<Double>,
    categoriaBuscada: String
): Double
```

Las funciones deberán:

* Utilizar ciclos para recorrer las listas.
* Considerar el caso en el que todavía no existan gastos.
* Evitar variables globales.
* Devolver resultados, no imprimirlos directamente.

También deberá programar una función para mostrar los resultados:

```kotlin
fun mostrarResumen(
    conceptos: List<String>,
    categorias: List<String>,
    montos: List<Double>
)
```

El resumen puede verse así:

```text
RESUMEN SEMANAL

Número de gastos: 4
Gasto total: $378.50
Promedio por gasto: $94.63
Gasto mayor: Libro de Kotlin, $180.00
```

### Commits obligatorios del estudiante B

```text
Agrega cálculos de total y gasto mayor
```

```text
Agrega cálculo por categoría y resumen semanal
```

Después ejecutará `push` de la rama `analisis-gastos`.

---

# Fase 5. Primera revisión mediante pull request

## Revisión del trabajo del estudiante A

1. El estudiante A crea un pull request:

```text
registro-gastos → main
```

2. En la descripción debe explicar:

```text
Funciones agregadas:
- Registro de concepto, categoría y monto.
- Validación de los datos ingresados.
- Presentación de todos los gastos.
```

3. El estudiante B revisa el código.
4. Debe escribir al menos un comentario concreto. Por ejemplo:

```text
¿Qué sucede si el usuario introduce texto cuando se solicita el monto?
```

5. El estudiante A atiende la observación.
6. Realiza un nuevo commit:

```text
Mejora validación del monto ingresado
```

7. Ejecuta `push`.
8. El estudiante B comprueba la corrección y aprueba el pull request.
9. El estudiante B realiza el `merge` hacia `main`.

Los pull requests permiten revisar y discutir los cambios antes de incorporarlos a la rama principal. [Documentación de GitHub sobre pull requests](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

---

# Fase 6. Actualización mediante pull

Después del primer `merge`, la rama remota `main` contiene código que el estudiante B todavía no tiene localmente.

## Actividad del estudiante B

1. Cambiar a la rama `main`.
2. Ejecutar:

```text
Git → Pull
```

3. Verificar que recibió las funciones desarrolladas por el estudiante A.
4. Regresar a la rama `analisis-gastos`.
5. Integrar los cambios actualizados de `main`:

```text
Git → Merge → main
```

6. Ejecutar el programa y corregir posibles errores de integración.
7. Ejecutar `push` de `analisis-gastos`.

Con esto se diferencia:

* `push`: envía commits locales a GitHub.
* `pull`: descarga e integra cambios del repositorio remoto.
* `merge`: integra el contenido de una rama en otra.

IntelliJ IDEA permite realizar `pull` desde `Git → Pull` y administrar las ramas desde sus paneles de control de versiones. [Guía oficial de sincronización de IntelliJ IDEA](https://www.jetbrains.com/help/idea/sync-with-a-remote-repository.html).

---

# Fase 7. Segundo pull request e intercambio de papeles

1. El estudiante B crea el pull request:

```text
analisis-gastos → main
```

2. El estudiante A revisa las funciones.
3. Debe verificar al menos estos casos:

| Prueba                | Resultado esperado                  |
| --------------------- | ----------------------------------- |
| Lista vacía           | No debe provocar un error           |
| Un solo gasto         | Debe ser identificado como el mayor |
| Varios gastos         | El total debe ser correcto          |
| Categoría inexistente | El total debe ser `0.0`             |
| Montos con decimales  | Deben calcularse correctamente      |

4. El estudiante A deja al menos un comentario.
5. El estudiante B realiza la corrección correspondiente.
6. Crea un nuevo commit.
7. Ejecuta `push`.
8. El estudiante A aprueba y realiza el `merge`.

De esta manera, ambos estudiantes habrán:

* Creado una rama.
* Realizado commits.
* Ejecutado `push`.
* Creado un pull request.
* Revisado código.
* Corregido código.
* Participado en un `merge`.

---

# Fase 8. Conflicto intencional

Esta fase se realizará después de integrar ambos trabajos.

## Preparación

Ambos estudiantes cambian a `main` y ejecutan `pull`.

Después crean ramas nuevas:

### Estudiante A

```text
titulo-estudiante-a
```

### Estudiante B

```text
titulo-estudiante-b
```

## Modificaciones

Los dos deberán cambiar exactamente la misma línea de `Main.kt`.

El estudiante A escribe:

```kotlin
println("CONTROL PERSONAL DE GASTOS")
```

El estudiante B escribe:

```kotlin
println("SISTEMA SEMANAL DE GASTOS")
```

Ambos realizan un commit y `push`.

### Orden de integración

1. El estudiante A crea su pull request.
2. El estudiante B lo revisa y fusiona con `main`.
3. El estudiante B intenta integrar su propia rama.
4. GitHub o IntelliJ IDEA deberá indicar que existe un conflicto.
5. Ambos estudiantes acuerdan que el resultado final será:

```kotlin
println("SISTEMA PERSONAL DE CONTROL DE GASTOS")
```

6. El estudiante B resuelve el conflicto.
7. Crea el commit:

```text
Resuelve conflicto en el título del programa
```

8. Ejecuta `push`.
9. El estudiante A revisa y aprueba el resultado.
10. Se realiza el `merge`.

Un conflicto aparece cuando Git no puede decidir automáticamente cuál de dos cambios incompatibles debe conservar. Debe resolverse antes de completar la fusión. [Explicación oficial de conflictos de GitHub](https://docs.github.com/en/pull-requests/reference/merge-conflicts).

---

# Fase 9. Integración del programa

Con todas las funciones disponibles, la pareja deberá completar el menú principal.

Una estructura inicial puede ser:

```kotlin
fun main() {
    val conceptos = mutableListOf<String>()
    val categorias = mutableListOf<String>()
    val montos = mutableListOf<Double>()

    var opcion: Int

    do {
        mostrarMenu()
        opcion = readln().toIntOrNull() ?: 0

        when (opcion) {
            1 -> registrarGasto(conceptos, categorias, montos)
            2 -> mostrarGastos(conceptos, categorias, montos)
            3 -> println("Total: $${calcularTotal(montos)}")
            4 -> mostrarGastoMayor(conceptos, categorias, montos)
            5 -> consultarGastosPorCategoria(categorias, montos)
            6 -> mostrarResumen(conceptos, categorias, montos)
            7 -> println("Programa terminado.")
            else -> println("Opción no válida.")
        }
    } while (opcion != 7)
}
```

Esta estructura es solamente una guía. La pareja debe completar las funciones faltantes y validar adecuadamente las entradas.

---

# Entregables

Cada pareja entregará:

1. Enlace al repositorio de GitHub.
2. Proyecto ejecutable en la rama `main`.
3. Historial con al menos ocho commits significativos.
4. Ramas creadas por ambos estudiantes.
5. Dos pull requests principales, uno por estudiante.
6. Comentarios de revisión realizados por ambos.
7. Evidencia del conflicto y de su resolución.
8. Archivo `README.md` con:

```text
Nombre del proyecto
Integrantes
Responsabilidades de cada integrante
Instrucciones para ejecutar el programa
Funciones implementadas
Conflicto encontrado y forma de resolverlo
Conclusión individual de cada integrante
```

## Evidencia individual

Cada estudiante agregará al `README.md` una breve reflexión:

* ¿Qué diferencia encontró entre `commit` y `push`?
* ¿Por qué debe hacerse `pull` antes de comenzar a modificar archivos?
* ¿Para qué sirve trabajar en ramas?
* ¿Qué ocasionó el conflicto?
* ¿Cómo decidió qué código conservar?
* ¿Qué aportó personalmente al programa?

# Criterios de evaluación

| Criterio                                                | Porcentaje |
| ------------------------------------------------------- | ---------: |
| Funcionamiento del programa en Kotlin                   |       30 % |
| Uso correcto de funciones, condiciones, ciclos y listas |       15 % |
| Organización del trabajo mediante ramas                 |       10 % |
| Calidad y distribución de los commits                   |       15 % |
| Uso de `push`, `pull` y `merge`                         |       10 % |
| Pull requests y revisión del compañero                  |       10 % |
| Resolución del conflicto                                |        5 % |
| README y reflexión individual                           |        5 % |
| **Total**                                               |  **100 %** |

## Condición de participación individual

La calificación no será necesariamente idéntica para ambos integrantes. Para obtener la totalidad de los puntos individuales, cada estudiante deberá aparecer en el historial del repositorio como autor de:

* Al menos tres commits funcionales.
* Una rama propia.
* Un pull request.
* Una corrección derivada de una revisión.
* Al menos un comentario de revisión al compañero.

No se considerará participación suficiente limitarse a descargar el proyecto, observar al compañero o realizar únicamente cambios de formato.
