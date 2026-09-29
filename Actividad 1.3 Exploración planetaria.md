# Actividad 1.3: Sistema de exploración de una misión planetaria 🪐

## Datos generales

**Modalidad:** individual  
**Lenguaje:** Kotlin  
**Entorno de desarrollo:** IntelliJ IDEA  
**Control de versiones:** Git y GitHub  
**Tipo de programa:** aplicación de consola

---

## Propósito

En esta actividad desarrollarás individualmente un **simulador de una misión de exploración planetaria**.

El objetivo es que apliques los conceptos de clases y objetos en Kotlin estudiados en clase, comenzando con el análisis del problema y avanzando progresivamente hacia una solución que utilice diferentes mecanismos de programación orientada a objetos y recursos propios de Kotlin.

Durante la actividad trabajarás con:

- clases y objetos;
- propiedades `val` y `var`;
- constructores;
- parámetros predeterminados;
- bloque `init`;
- getters y setters personalizados;
- funciones miembro;
- herencia;
- `open` y `override`;
- clases abstractas;
- interfaces;
- funciones de extensión;
- `data class`;
- `enum class`;
- `object`;
- `companion object`;
- paquetes;
- modificadores de visibilidad.

> **Importante:** no se busca solamente obtener un programa que funcione. Tu repositorio deberá mostrar el proceso seguido para analizar, diseñar, implementar y probar tu solución.

---

# 1. Situación problemática

Una agencia científica prepara una misión para explorar la superficie de un planeta.

Para realizar la exploración dispone de diferentes **vehículos exploradores**.

Todos ellos comparten algunas características. Por ejemplo:

- tienen un nombre;
- disponen de un determinado nivel de energía;
- pueden desplazarse;
- recorren cierta distancia;
- participan en actividades de exploración.

Sin embargo, no todos realizan las mismas actividades.

La misión contará inicialmente con dos tipos de exploradores:

### Rover terrestre

Se desplaza sobre la superficie del planeta y puede analizar las zonas que encuentra durante su recorrido.

### Dron explorador

Puede desplazarse y realizar vuelos de reconocimiento para analizar zonas desde el aire.

Durante la misión, los exploradores pueden encontrar diferentes tipos de zonas:

```text
SEGURA
ROCOSA
PELIGROSA
```

También pueden realizar descubrimientos científicos, por ejemplo:

```text
Agua congelada
Formación mineral
Cráter
Posible material orgánico
```

La misión contará además con un **centro de control**, encargado de registrar información general sobre las operaciones realizadas.

Tu tarea será diseñar e implementar un programa en Kotlin que permita representar y simular este sistema.

> Las reglas utilizadas en esta actividad son simplificaciones con fines didácticos. No necesitas investigar sobre robótica, exploración espacial o funcionamiento real de vehículos planetarios.

---

# 2. Reglas generales del simulador

## Energía

Todos los exploradores tendrán un nivel de energía entre:

```text
0 y 100 %
```

Tu programa deberá impedir que un explorador conserve valores fuera de ese intervalo.

## Desplazamiento

Los exploradores podrán desplazarse.

Al hacerlo:

- aumentará la distancia recorrida;
- disminuirá su nivel de energía.

Tú deberás establecer y documentar las reglas utilizadas para calcular este consumo.

## Exploración

Los exploradores podrán analizar zonas.

El comportamiento podrá ser diferente dependiendo del tipo de explorador.

## Descubrimientos

Durante una exploración podrá registrarse un descubrimiento con información como:

- tipo;
- descripción;
- zona en la que fue encontrado.

## Centro de control

Durante toda la ejecución deberá existir un único centro de control de la misión.

---

# 3. Desarrollo de la actividad

La actividad se desarrollará por fases.

No avances directamente hasta el programa terminado. El historial de tu repositorio deberá permitir observar cómo evolucionó tu solución.

---

# Fase 1. Creación del proyecto, repositorio y análisis del problema

## 1.1 Crea el proyecto en IntelliJ IDEA

Abre **IntelliJ IDEA** y crea un nuevo proyecto **Kotlin** llamado:

```text
ExploracionPlanetaria
```

Crea un programa mínimo:

```kotlin
fun main() {
    println("Misión de exploración planetaria")
}
```

Ejecuta el programa y comprueba que no existan errores.

---

## 1.2 Activa Git en IntelliJ IDEA

Todavía en **IntelliJ IDEA**, activa el control de versiones:

```text
VCS
   ↓
Enable Version Control Integration
   ↓
Git
```

A partir de este momento tendrás un **repositorio Git local** asociado con tu proyecto.

> Esto todavía no significa que tu proyecto esté publicado en GitHub.

Realiza tu primer `commit`:

```text
Inicializa proyecto Kotlin
```

Recuerda:

```text
COMMIT
   ↓
registra una versión de tu trabajo
en el repositorio Git local
```

---

## 1.3 Crea el repositorio en GitHub

Ahora abre **GitHub desde tu navegador web**.

Crea en tu cuenta un repositorio público llamado:

```text
exploracion-planetaria-kotlin
```

### Importante

Crea el repositorio **vacío**.

En este momento no agregues desde GitHub:

- `README.md`;
- `.gitignore`;
- licencia.

> Este paso se realiza en la página web de GitHub, no en IntelliJ IDEA.

Una vez creado, copia la dirección HTTPS del repositorio. Tendrá una forma semejante a:

```text
https://github.com/TU-USUARIO/exploracion-planetaria-kotlin.git
```

---

## 1.4 Vincula tu proyecto con GitHub

Regresa a **IntelliJ IDEA**.

Selecciona:

```text
Git
   ↓
Manage Remotes...
```

Presiona:

```text
+
```

Agrega:

```text
Name: origin

URL:
https://github.com/TU-USUARIO/exploracion-planetaria-kotlin.git
```

Presiona **OK**.

Ahora tu proyecto tiene la siguiente relación:

```text
Proyecto en IntelliJ IDEA
          │
          ▼
Repositorio Git local
          │
          │ origin
          ▼
Repositorio remoto
       en GitHub
```

---

## 1.5 Publica tu primer avance

En IntelliJ IDEA selecciona:

```text
Git
   ↓
Push...
```

Realiza el `push`.

Recuerda la diferencia:

```text
COMMIT
   ↓
registra cambios en tu repositorio local

PUSH
   ↓
envía tus commits al repositorio
remoto en GitHub
```

Abre ahora **GitHub desde el navegador**, actualiza la página y comprueba que aparezcan los archivos del proyecto y el commit:

```text
Inicializa proyecto Kotlin
```

No continúes hasta comprobar que tu proyecto se encuentra publicado correctamente.

---

## 1.6 Crea tu documento de análisis

Regresa a **IntelliJ IDEA**.

Crea:

```text
docs/01-analisis.md
```

Este archivo documentará tus decisiones durante la actividad.

Agrega:

```markdown
# Análisis del sistema

## Descripción del problema
```

Explica con tus propias palabras:

- ¿qué sistema vas a representar?;
- ¿qué elementos intervienen?;
- ¿qué información necesita conservar el sistema?;
- ¿qué operaciones deberá realizar?

---

## 1.7 Identifica objetos y responsabilidades

Agrega:

```markdown
## Objetos y responsabilidades
```

Completa:

| Objeto propuesto | Información que conserva | Comportamientos | Responsabilidad |
|---|---|---|---|
| ... | ... | ... | ... |
| ... | ... | ... | ... |

Después responde:

1. ¿Qué características tienen en común el rover y el dron?
2. ¿Qué características son diferentes?
3. ¿Existe un concepto más general que permita representar a ambos?
4. ¿Qué elementos parecen representar capacidades y no necesariamente tipos de objetos?
5. ¿Qué información pertenece a un explorador particular y cuál podría ser compartida?

> **Todavía no implementes las clases definitivas.**

Realiza:

```text
Commit:
Documenta análisis inicial del sistema
```

y después:

```text
Push
```

Comprueba desde GitHub que el documento aparezca en tu repositorio.

---

# Fase 2. Clases, objetos y constructores

Ahora comenzarás la implementación.

## 2.1 Diseña la clase inicial

A partir de tu análisis, crea una clase que permita representar inicialmente un explorador.

Considera información como:

- nombre;
- energía;
- distancia recorrida.

Decide cuáles propiedades deberán declararse mediante:

```kotlin
val
```

y cuáles mediante:

```kotlin
var
```

No copies automáticamente los nombres anteriores. Decide qué necesita tu solución.

---

## 2.2 Utiliza un constructor primario

Define las propiedades necesarias utilizando un **constructor primario**.

Crea al menos dos instancias con datos diferentes.

Comprueba que cada objeto conserva su propio estado.

En `docs/01-analisis.md` responde:

> ¿Qué diferencia existe entre la clase que definiste y los objetos que creaste a partir de ella?

---

## 2.3 Experimenta con `val` y `var`

Modifica durante la ejecución alguna propiedad declarada mediante `var`.

Después intenta modificar una propiedad declarada mediante `val`.

Observa lo que indica IntelliJ IDEA.

No dejes en la versión final código que impida compilar el programa.

Documenta:

> ¿Por qué decidiste utilizar `val` o `var` para cada una de las propiedades principales de tu clase?

---

## 2.4 Utiliza parámetros predeterminados

Al menos un parámetro del constructor deberá tener un valor predeterminado.

Crea objetos:

- proporcionando todos los argumentos;
- utilizando el valor predeterminado;
- utilizando argumentos con nombre.

Explica:

> ¿Qué ventaja ofrecen los parámetros predeterminados?

---

## 2.5 Utiliza un bloque `init`

Agrega un bloque:

```kotlin
init {
    // ...
}
```

Utilízalo para realizar una inicialización o comprobación relacionada con el estado inicial del objeto.

Documenta:

> ¿Cuándo se ejecuta el bloque `init`?

### Commits de la fase

Realiza commits que reflejen tu avance. Por ejemplo:

```text
Implementa clase inicial y constructor primario
```

```text
Agrega parámetros predeterminados e inicialización
```

Realiza `push` después de avances significativos.

---

# Fase 3. Propiedades, encapsulación y comportamiento

## 3.1 Controla el nivel de energía

El nivel de energía solamente puede encontrarse entre:

```text
0 y 100
```

Utiliza un **setter personalizado** para controlar los valores asignados.

Comprueba qué sucede si intentas asignar:

```text
120
```

o:

```text
-20
```

El objeto no deberá conservar un nivel de energía inválido.

---

## 3.2 Crea una propiedad calculada

Agrega al menos una propiedad cuyo resultado se obtenga mediante un **getter personalizado**.

La propiedad deberá calcular información a partir del estado actual del objeto.

Evita almacenar como propiedad independiente algo que pueda calcularse a partir de otros datos.

---

## 3.3 Agrega funciones miembro

Los objetos deberán realizar acciones mediante funciones.

Implementa comportamientos relacionados con:

- desplazarse;
- consumir energía;
- mostrar información.

Las responsabilidades deberán estar dentro de las clases correspondientes.

Evita realizar toda la lógica directamente desde `main()`.

---

## 3.4 Controla la visibilidad

Analiza qué propiedades o funciones realmente necesitan ser visibles desde otras partes del programa.

Utiliza de manera justificada:

```kotlin
private
```

y, cuando posteriormente construyas la jerarquía:

```kotlin
protected
```

En tu documento responde:

1. ¿Qué información protegiste mediante `private`?
2. ¿Por qué no debe modificarse directamente desde `main()`?
3. ¿Qué información necesita estar disponible para las subclases?

### Commits sugeridos

```text
Agrega propiedades controladas y encapsulación
```

```text
Implementa comportamiento de los exploradores
```

---

# Fase 4. Herencia y clases abstractas

Hasta este momento has trabajado con un concepto general de explorador.

Ahora diferenciarás los tipos de vehículos.

## 4.1 Analiza la jerarquía

Antes de modificar tu código, agrega a `docs/01-analisis.md`:

```markdown
## Diseño de la jerarquía
```

Explica:

- qué características comparten todos los exploradores;
- qué comportamientos son comunes;
- qué comportamientos pueden variar;
- qué características son exclusivas del rover;
- qué características son exclusivas del dron.

---

## 4.2 Crea una clase abstracta

Representa el concepto general mediante una clase:

```text
Explorador
```

que sea:

```kotlin
abstract
```

La clase deberá contener el estado y comportamiento común.

Incluye al menos:

- propiedades comunes;
- una función implementada que puedan utilizar las subclases;
- una propiedad o función abstracta que las subclases deban proporcionar.

---

## 4.3 Crea las subclases

Implementa:

```text
RoverTerrestre
```

y:

```text
DronExplorador
```

como subclases de `Explorador`.

No repitas en las subclases propiedades que ya pertenecen a la superclase.

---

## 4.4 Utiliza `open` y `override`

Algunos comportamientos podrán tener una implementación general y ser redefinidos posteriormente.

Utiliza:

```kotlin
open
```

para permitir que un comportamiento pueda sobrescribirse y:

```kotlin
override
```

para proporcionar la implementación correspondiente.

Demuestra durante la ejecución que el rover y el dron pueden responder de manera diferente a una misma operación.

En tu documento responde:

1. ¿Por qué `Explorador` es una clase abstracta?
2. ¿Qué heredaron `RoverTerrestre` y `DronExplorador`?
3. ¿Qué comportamiento sobrescribiste?
4. ¿Por qué fue necesario utilizar `open` y `override`?

### Commits sugeridos

```text
Reorganiza exploradores mediante herencia
```

```text
Implementa clase abstracta y subclases
```

```text
Agrega sobrescritura de comportamiento
```

---

# Fase 5. Interfaces

La herencia permite expresar qué **es** un objeto. Sin embargo, algunas características pueden representar una **capacidad** que diferentes objetos pueden ofrecer.

## 5.1 Diseña una interfaz

Crea una interfaz relacionada con alguna capacidad de exploración.

Por ejemplo, podrías representar la capacidad de:

```text
analizar una zona
```

Una posible estructura sería:

```kotlin
interface Analizable {
    fun analizarZona(zona: TipoZona)
}
```

Este ejemplo sirve como referencia. Puedes proponer otro nombre o comportamiento si resulta más adecuado para tu solución.

---

## 5.2 Implementa la interfaz

Haz que las clases correspondientes implementen la interfaz.

Utiliza:

```kotlin
override
```

para proporcionar el comportamiento requerido.

Crea objetos de diferentes tipos y demuestra que pueden cumplir el mismo contrato.

En `docs/01-analisis.md` responde:

1. ¿Qué capacidad representa tu interfaz?
2. ¿Qué clases la implementan?
3. ¿Por qué utilizaste una interfaz en lugar de otra superclase?
4. ¿Qué diferencia existe entre lo que representa `Explorador` y lo que representa tu interfaz?

### Commit sugerido

```text
Implementa capacidad de exploración mediante interfaz
```

Realiza `push`.

---

# Fase 6. Recursos específicos de Kotlin

## 6.1 Utiliza `enum class`

Representa los posibles tipos de zona mediante:

```kotlin
enum class TipoZona {
    SEGURA,
    ROCOSA,
    PELIGROSA
}
```

Utiliza `TipoZona` en las clases correspondientes.

En tu documento responde:

> ¿Qué ventaja ofrece utilizar `TipoZona` en lugar de representar estos estados mediante `String`?

---

## 6.2 Utiliza una `data class`

Crea una `data class` para representar un descubrimiento científico.

Deberá almacenar información como:

- tipo;
- descripción;
- zona.

Crea al menos dos descubrimientos.

Imprime directamente uno de ellos:

```kotlin
println(descubrimiento)
```

Observa el resultado.

Después utiliza:

```kotlin
copy()
```

para crear otro objeto a partir de un descubrimiento existente modificando alguno de sus datos.

Responde:

1. ¿Por qué `Descubrimiento` es un buen candidato para una `data class`?
2. ¿Qué comportamiento proporciona Kotlin automáticamente?
3. ¿Qué hace `copy()`?

---

# Fase 7. Funciones de extensión

Ahora agregarás funcionalidad a un tipo **sin modificar la definición de su clase**.

## 7.1 Crea una función de extensión

Diseña una función de extensión que tenga una utilidad dentro de tu programa.

Por ejemplo:

```kotlin
fun Double.comoDistancia(): String {
    return "$this km"
}
```

permitiría escribir:

```kotlin
println(12.5.comoDistancia())
```

Puedes utilizar esta propuesta o crear otra extensión que resulte coherente con tu solución.

La función deberá:

- extender un tipo existente;
- resolver una necesidad concreta;
- utilizarse durante la simulación.

En tu documento responde:

1. ¿Qué tipo extendiste?
2. ¿Qué funcionalidad agregaste?
3. ¿Modificaste realmente la clase original?
4. ¿Puede la extensión acceder directamente a los miembros `private` de esa clase?

### Commits sugeridos

```text
Agrega enum y data class para datos de misión
```

```text
Implementa función de extensión
```

---

# Fase 8. `object` y `companion object`

Aunque ambos utilizan objetos, representan necesidades diferentes.

Deberás utilizar los dos y explicar su diferencia.

## 8.1 Crea el centro de control mediante `object`

Durante la simulación deberá existir **un único centro de control**.

Representa:

```text
CentroControl
```

mediante:

```kotlin
object CentroControl {
    // ...
}
```

Asígnale responsabilidades relacionadas con la misión. Por ejemplo:

- registrar operaciones;
- mostrar mensajes;
- registrar descubrimientos;
- proporcionar un resumen de la misión.

Selecciona únicamente las responsabilidades que sean coherentes con tu diseño.

Utiliza `CentroControl` desde diferentes partes del programa.

No deberás crear instancias mediante un constructor.

---

## 8.2 Utiliza un `companion object`

Ahora identifica una propiedad o función que esté directamente relacionada con una clase pero que sea **compartida por todas sus instancias**.

Utiliza:

```kotlin
companion object {
    // ...
}
```

Por ejemplo, podrías utilizarlo para llevar un contador de exploradores creados.

Si existen:

```text
Ares
Ícaro
Odiseo
```

el elemento compartido deberá permitir conocer que existen:

```text
3 exploradores
```

Puedes proponer otro uso si resulta más apropiado para tu diseño.

Accede a ese elemento mediante el nombre de la clase.

---

## 8.3 Compara ambos recursos

En `docs/01-analisis.md` responde:

1. ¿Por qué utilizaste `object` para `CentroControl`?
2. ¿Por qué no necesitas crear diferentes instancias?
3. ¿Qué colocaste dentro del `companion object`?
4. ¿Por qué esa información pertenece a la clase y no a un explorador particular?
5. ¿Cuál es la diferencia entre `CentroControl` y el `companion object` de tu programa?

### Commits sugeridos

```text
Implementa CentroControl mediante object
```

```text
Agrega comportamiento compartido con companion object
```

Realiza `push` y comprueba desde **GitHub en el navegador** que tus commits estén publicados.

---

# Fase 9. Organización mediante paquetes

Organiza las clases de tu programa mediante paquetes.

Una posible organización sería:

```text
exploracion
│
├── exploradores
├── modelo
├── control
└── utilidades
```

No estás obligado a utilizar exactamente esta estructura.

La organización deberá corresponder con las responsabilidades de tus clases.

Utiliza correctamente:

```kotlin
package ...
```

e:

```kotlin
import ...
```

cuando sea necesario.

Los nombres de los paquetes deberán escribirse en minúsculas.

En tu documento explica brevemente el criterio que utilizaste para organizar las clases.

### Commit sugerido

```text
Organiza código mediante paquetes
```

---

# Fase 10. Integración y pruebas

## 10.1 Integra la simulación

Tu programa final deberá crear como mínimo:

- un `RoverTerrestre`;
- un `DronExplorador`;
- diferentes zonas;
- al menos dos descubrimientos.

Durante la ejecución deberás demostrar:

- creación de objetos;
- propiedades `val` y `var`;
- constructor primario;
- parámetros predeterminados;
- `init`;
- getter personalizado;
- setter personalizado;
- funciones miembro;
- encapsulación;
- herencia;
- clase abstracta;
- `open`;
- `override`;
- interfaz;
- `enum class`;
- `data class`;
- `copy()`;
- función de extensión;
- `object`;
- `companion object`;
- paquetes;
- modificadores de visibilidad.

`main()` deberá coordinar la simulación.

Evita colocar en `main()` lógica que corresponda a las responsabilidades de otros objetos.

---

## 10.2 Realiza pruebas

Comprueba como mínimo:

| Prueba | Resultado esperado |
|---|---|
| Crear dos exploradores | Cada objeto conserva su propio estado |
| Utilizar un parámetro predeterminado | Se utiliza correctamente el valor establecido |
| Asignar energía mayor a 100 | No se conserva un valor inválido |
| Asignar energía menor a 0 | No se conserva un valor inválido |
| Crear un rover | Hereda las características comunes |
| Crear un dron | Hereda las características comunes |
| Ejecutar comportamiento sobrescrito | Cada tipo responde de acuerdo con su implementación |
| Utilizar la interfaz | Las clases correspondientes cumplen el contrato |
| Utilizar `TipoZona.ROCOSA` | Se utiliza correctamente el `enum` |
| Crear un descubrimiento | La `data class` conserva sus datos |
| Utilizar `copy()` | Se obtiene un nuevo objeto con la modificación |
| Ejecutar la función de extensión | Produce el resultado esperado |
| Utilizar `CentroControl` desde diferentes puntos | Se utiliza el mismo objeto |
| Crear varios exploradores | El elemento del `companion object` se comparte correctamente |

Agrega **dos pruebas adicionales diseñadas por ti**.

Documenta brevemente qué probaste y cuál fue el resultado.

### Commits sugeridos

```text
Integra simulación completa
```

```text
Agrega pruebas del sistema
```

Realiza `push`.

---

# Fase 11. Documentación final

## 11.1 Completa el `README.md`

Tu repositorio deberá incluir un archivo:

```text
README.md
```

con:

### Nombre del proyecto

### Descripción

Explica brevemente qué simula el programa.

### Estructura

Describe las principales clases, interfaces y objetos.

### Ejecución

Explica cómo ejecutar el programa.

### Conceptos aplicados

Completa:

| Concepto | ¿Dónde lo utilicé? | ¿Por qué lo utilicé? |
|---|---|---|
| Constructor primario | ... | ... |
| Parámetros predeterminados | ... | ... |
| `init` | ... | ... |
| Getter personalizado | ... | ... |
| Setter personalizado | ... | ... |
| Herencia | ... | ... |
| Clase abstracta | ... | ... |
| `open` / `override` | ... | ... |
| Interfaz | ... | ... |
| `data class` | ... | ... |
| `enum class` | ... | ... |
| Función de extensión | ... | ... |
| `object` | ... | ... |
| `companion object` | ... | ... |
| `private` / `protected` | ... | ... |
| Paquetes | ... | ... |

No escribas únicamente la definición del concepto.

Indica **dónde puede observarse en tu propio programa y por qué decidiste utilizarlo**.

---

# Reflexión final

Agrega al `README.md`:

```markdown
## Reflexión final
```

Responde con tus propias palabras:

1. ¿Qué diferencia existe entre una clase y un objeto?
2. ¿Qué diferencia encontraste entre `val` y `var`?
3. ¿Qué ventaja ofrecen los parámetros predeterminados?
4. ¿Para qué utilizaste `init`?
5. ¿Por qué utilizaste una clase abstracta para representar a los exploradores?
6. ¿Qué comportamiento heredaron las subclases?
7. ¿Qué comportamiento sobrescribiste mediante `override`?
8. ¿Qué representa la interfaz de tu programa?
9. ¿Por qué esa capacidad se representó mediante una interfaz y no mediante herencia?
10. ¿Qué ventaja tuvo utilizar una `data class`?
11. ¿Qué ventaja tuvo utilizar una `enum class`?
12. ¿Qué hace la función de extensión que implementaste?
13. ¿Qué representa `object CentroControl`?
14. ¿Qué colocaste en el `companion object` y por qué?
15. ¿Cuál es la diferencia entre `object` y `companion object` en tu programa?
16. ¿Qué información protegiste mediante modificadores de visibilidad?
17. ¿Cómo organizaste tu programa mediante paquetes?
18. Si tuvieras que agregar un nuevo tipo de explorador, ¿qué partes del programa tendrías que modificar?

### Commit final sugerido

```text
Completa documentación y reflexión final
```

Realiza `push` y comprueba desde GitHub que la versión final esté publicada.

---

# Entregables

Deberás entregar:

1. enlace al repositorio público de GitHub;
2. proyecto Kotlin funcional;
3. `docs/01-analisis.md`;
4. código organizado mediante paquetes;
5. clase abstracta y subclases;
6. interfaz;
7. propiedades, constructores y funciones miembro;
8. getter y setter personalizados;
9. `data class`;
10. `enum class`;
11. función de extensión;
12. `object`;
13. `companion object`;
14. pruebas realizadas;
15. `README.md`;
16. historial de commits que permita observar el desarrollo de la actividad.

---

# Criterios de evaluación

| Criterio | Porcentaje |
|---|---:|
| Clases, objetos, propiedades y constructores | 20 % |
| Herencia, clase abstracta, interfaz y sobrescritura | 25 % |
| Recursos específicos de Kotlin | 25 % |
| Organización, visibilidad e integración | 10 % |
| Análisis y pruebas | 10 % |
| GitHub, proceso y documentación | 10 % |
| **Total** | **100 %** |

## Clases, objetos, propiedades y constructores — 20 %

Se evaluará:

- creación correcta de clases e instancias;
- uso justificado de `val` y `var`;
- constructor primario;
- parámetros predeterminados;
- `init`;
- propiedades;
- getters y setters personalizados;
- funciones miembro.

## Herencia, clase abstracta, interfaz y sobrescritura — 25 %

Se evaluará:

- jerarquía coherente;
- reutilización mediante herencia;
- clase abstracta;
- uso correcto de `open`;
- uso correcto de `override`;
- interfaz;
- implementación del contrato;
- diferenciación entre herencia e interfaz;
- ausencia de duplicación innecesaria.

## Recursos específicos de Kotlin — 25 %

Se evaluará el uso y comprensión de:

- `data class`;
- `copy()`;
- `enum class`;
- función de extensión;
- `object`;
- `companion object`.

No será suficiente agregar estos recursos únicamente para cumplir el requisito. Deberán tener una función identificable dentro de la solución.

## Organización, visibilidad e integración — 10 %

Se evaluará:

- organización mediante paquetes;
- uso apropiado de `private` y `protected`;
- distribución adecuada de responsabilidades;
- integración del sistema;
- uso de `main()` principalmente para coordinar la simulación.

## Análisis y pruebas — 10 %

Se evaluará:

- análisis realizado antes de la implementación;
- identificación de objetos y responsabilidades;
- análisis de características comunes;
- justificación de decisiones;
- pruebas solicitadas;
- dos pruebas adicionales.

## GitHub, proceso y documentación — 10 %

Se evaluará:

- repositorio correctamente publicado;
- commits significativos;
- uso de `push` durante el desarrollo;
- `docs/01-analisis.md`;
- `README.md`;
- evidencia de conceptos;
- reflexión individual;
- historial que permita observar la evolución del trabajo.

---

# Condición de trabajo individual

Esta actividad es **individual**.

El historial del repositorio deberá permitir observar tu proceso de trabajo.

Deberá existir evidencia de una secuencia semejante a:

```text
Creación del proyecto
        ↓
Análisis
        ↓
Clases y propiedades
        ↓
Encapsulación
        ↓
Herencia
        ↓
Interfaz
        ↓
Recursos específicos de Kotlin
        ↓
Integración
        ↓
Pruebas
        ↓
Documentación
```

La evidencia del análisis deberá aparecer en el historial **antes de la implementación correspondiente**.

No se considerará evidencia suficiente subir todo el proyecto terminado mediante un único commit.

> El objetivo de la actividad no es solamente entregar un programa que funcione. Tu repositorio deberá mostrar cómo analizaste el problema, cómo tomaste decisiones de diseño y cómo construiste progresivamente tu solución.
