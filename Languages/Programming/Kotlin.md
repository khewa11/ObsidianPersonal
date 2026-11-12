# Kotlin

Lenguaje moderno, conciso y seguro, desarrollado por JetBrains. Corre en la JVM, Android, JS, Native y multiplataforma (KMP). Es el lenguaje oficial para Android.

---

# Parte 1: Sintaxis básica

## 1. Hola mundo

```kotlin
fun main() {
    println("Hola, Kotlin")
}
```

- No hay `;` obligatorio al final de línea.
- `main` es el punto de entrada. También puede recibir `args: Array<String>`.

## 2. Variables

```kotlin
val nombre = "Ana"        // inmutable (solo lectura), preferir siempre
var edad = 30             // mutable
edad = 31

val pi: Double = 3.14159  // tipo explícito (opcional, hay inferencia)
const val MAX = 100       // constante en compilación (top-level u object)
```

> Regla: usa `val` por defecto, `var` solo si realmente cambia.

## 3. Tipos básicos

| Tipo | Ejemplo |
|---|---|
| `Int`, `Long` | `42`, `42L` |
| `Double`, `Float` | `3.14`, `3.14f` |
| `Boolean` | `true`, `false` |
| `Char` | `'a'` |
| `String` | `"texto"` |

```kotlin
val x: Int = 10
val y: Double = x.toDouble()   // no hay conversión implícita
val s = "Edad: $edad"          // plantilla de string
val t = "Doble: ${edad * 2}"   // expresión en plantilla
val multi = """
    Texto
    multilínea
""".trimIndent()
```

## 4. Null safety (lo más importante de Kotlin)

Por defecto los tipos **no** aceptan `null`. Se añade `?` para permitirlo.

```kotlin
var a: String = "hola"
// a = null            // ERROR de compilación
var b: String? = null  // OK

b?.length              // safe call: devuelve null si b es null
b?.length ?: 0         // elvis: valor por defecto
b!!.length             // "confía en mí": lanza NPE si es null (evitar)

b?.let { println(it) } // ejecuta el bloque solo si no es null

if (b != null) {
    println(b.length)  // smart cast: aquí b ya es String
}
```

## 5. Operadores

```kotlin
+  -  *  /  %          // aritméticos
==  !=  <  >  <=  >=   // comparación (== compara contenido, equivale a equals)
===                    // igualdad de referencia
&&  ||  !              // lógicos
a..b                   // rango inclusivo
a until b              // rango sin incluir b
```

## 6. Control de flujo

### if es una expresión

```kotlin
val mayor = if (edad >= 18) "mayor" else "menor"
```

### when (el "switch" potente)

```kotlin
when (x) {
    1 -> println("uno")
    2, 3 -> println("dos o tres")
    in 4..10 -> println("entre 4 y 10")
    is String -> println("es un String")
    else -> println("otro")
}

val texto = when {
    edad < 13 -> "niño"
    edad < 18 -> "adolescente"
    else -> "adulto"
}
```

### Bucles

```kotlin
for (i in 1..5) println(i)             // 1,2,3,4,5
for (i in 0 until 5) println(i)        // 0..4
for (i in 10 downTo 0 step 2) println(i)
for (item in lista) println(item)
for ((i, item) in lista.withIndex()) println("$i: $item")

while (cond) { }
do { } while (cond)

break; continue                        // igual que otros lenguajes
```

## 7. Funciones

```kotlin
fun sumar(a: Int, b: Int): Int {
    return a + b
}

fun sumar2(a: Int, b: Int) = a + b             // función de expresión

fun saludar(nombre: String = "mundo") {        // parámetro por defecto
    println("Hola, $nombre")
}

saludar()                                      // Hola, mundo
saludar(nombre = "Ana")                        // argumento nombrado

fun varios(vararg nums: Int) = nums.sum()      // número variable de args
```

- Sin tipo de retorno => `Unit` (equivale a `void`).
- Funciones locales (dentro de otras) están permitidas.

### Lambdas y funciones de orden superior

```kotlin
val doble = { x: Int -> x * 2 }
doble(4) // 8

fun aplicar(n: Int, f: (Int) -> Int) = f(n)
aplicar(5) { it * 3 }          // 'it' = único parámetro; lambda final fuera de ()
```

### Funciones de extensión

Añaden métodos a clases existentes sin heredar.

```kotlin
fun String.esPalindromo() = this == this.reversed()
"oso".esPalindromo() // true
```

## 8. Clases y objetos

```kotlin
class Persona(val nombre: String, var edad: Int) {   // constructor primario
    fun saludar() = println("Soy $nombre")
}

val p = Persona("Ana", 30)    // sin 'new'
p.saludar()
```

- Las clases son `final` por defecto; usa `open` para poder heredar.
- Visibilidad: `public` (default), `private`, `protected`, `internal` (mismo módulo).

```kotlin
class Usuario(val nombre: String) {
    init { println("Creado $nombre") }              // bloque de inicialización
    constructor() : this("anónimo")                 // constructor secundario
}
```

### Herencia e interfaces

```kotlin
interface Volador { fun volar() }

open class Animal(val nombre: String) {
    open fun sonido() = "..."
}

class Perro(nombre: String) : Animal(nombre) {
    override fun sonido() = "Guau"
}
```

### data class

Genera `equals`, `hashCode`, `toString`, `copy` y desestructuración.

```kotlin
data class Usuario(val id: Int, val nombre: String)

val u = Usuario(1, "Ana")
val u2 = u.copy(nombre = "Luis")
val (id, nombre) = u            // desestructuración
```

### object y companion object

```kotlin
object Config {                 // singleton
    val url = "https://api.com"
}

class Foo {
    companion object {          // equivalente a "static"
        fun crear() = Foo()
    }
}
```

### enum y sealed class

```kotlin
enum class Direccion { NORTE, SUR, ESTE, OESTE }

sealed interface Resultado {                 // jerarquía cerrada
    data class Exito(val datos: String) : Resultado
    data class Error(val msg: String) : Resultado
    data object Cargando : Resultado
}

fun manejar(r: Resultado) = when (r) {       // when exhaustivo, sin else
    is Resultado.Exito -> r.datos
    is Resultado.Error -> r.msg
    Resultado.Cargando -> "..."
}
```

> `sealed` es la base para modelar **estados de UI**.

### Propiedades con getter/setter

```kotlin
class Rect(val w: Int, val h: Int) {
    val area: Int get() = w * h
}
```

## 9. Colecciones

```kotlin
val lista = listOf(1, 2, 3)               // inmutable
val mutable = mutableListOf(1, 2, 3)
mutable.add(4)

val conjunto = setOf(1, 2, 2)             // {1, 2}
val mapa = mapOf("a" to 1, "b" to 2)
val mm = mutableMapOf<String, Int>()
mm["c"] = 3
```

### Operaciones funcionales

```kotlin
val nums = listOf(1, 2, 3, 4, 5, 6)

nums.filter { it % 2 == 0 }        // [2, 4, 6]
nums.map { it * 2 }                // [2, 4, 6, 8, 10, 12]
nums.sum()
nums.first(); nums.last()
nums.find { it > 3 }               // 4 (o null)
nums.any { it > 5 }; nums.all { it > 0 }
nums.groupBy { it % 2 }            // {1=[1,3,5], 0=[2,4,6]}
nums.sortedByDescending { it }
nums.take(3); nums.drop(3)
nums.forEach { println(it) }
nums.fold(0) { acc, n -> acc + n }
```

## 10. Scope functions

| Función | Referencia | Devuelve | Uso típico |
|---|---|---|---|
| `let` | `it` | resultado lambda | null-check, transformar |
| `run` | `this` | resultado lambda | calcular algo con el objeto |
| `with` | `this` | resultado lambda | operar sobre un objeto |
| `apply` | `this` | el objeto | configurar objeto |
| `also` | `it` | el objeto | efectos secundarios (log) |

```kotlin
val p = Persona("Ana", 30).apply { edad = 31 }
nombre?.let { println(it) }
```

## 11. Manejo de errores

```kotlin
try {
    val n = "abc".toInt()
} catch (e: NumberFormatException) {
    println("No es número")
} finally {
    println("siempre")
}

val n = "abc".toIntOrNull() ?: 0      // alternativa idiomática
require(edad >= 0) { "Edad inválida" }  // lanza IllegalArgumentException
```

`try` también es una expresión: `val x = try { ... } catch (e: Exception) { 0 }`.

## 12. Genéricos

```kotlin
class Caja<T>(val valor: T)
fun <T> primero(l: List<T>): T = l.first()
val c = Caja<Int>(5)
```

## 13. Corrutinas (asincronía)

Dependencia: `org.jetbrains.kotlinx:kotlinx-coroutines-core`.

```kotlin
suspend fun cargarDatos(): String {     // se puede pausar sin bloquear
    delay(1000)
    return "datos"
}

fun main() = runBlocking {
    val r = cargarDatos()
    println(r)
}

// Concurrencia
coroutineScope {
    val a = async { cargarDatos() }
    val b = async { cargarDatos() }
    println(a.await() + b.await())
}

launch { /* dispara y olvida */ }
withContext(Dispatchers.IO) { /* cambiar de hilo */ }
```

- `Dispatchers.Main` (UI), `Dispatchers.IO` (red/disco), `Dispatchers.Default` (CPU).
- Una función `suspend` solo se llama desde otra `suspend` o desde un `launch`/`async`.

### Flow (flujo de valores en el tiempo)

```kotlin
fun contador(): Flow<Int> = flow {
    for (i in 1..3) { delay(500); emit(i) }
}

contador().collect { println(it) }

// StateFlow: estado observable con valor actual (clave en UI)
val _estado = MutableStateFlow(0)
val estado: StateFlow<Int> = _estado.asStateFlow()
_estado.value = 5
```

## 14. Otros imprescindibles

```kotlin
// Imports y paquetes
package com.ejemplo.app
import kotlin.math.max

// typealias
typealias Callback = (String) -> Unit

// Delegación de propiedades
val perezoso by lazy { calcularCostoso() }   // se evalúa al primer uso
lateinit var servicio: Servicio              // inicialización tardía (no null)

// Inline value class
@JvmInline value class UserId(val v: Int)
```

---

# Parte 2: Screens y UI (Jetpack Compose)

La UI moderna de Android se hace con **Jetpack Compose**: UI **declarativa** escrita en Kotlin (sin XML). Describes *cómo se ve la UI para un estado dado*, y Compose la redibuja cuando el estado cambia.

> `UI = f(estado)`

(Con **Compose Multiplatform** se usa casi lo mismo para Desktop, iOS y Web.)

## 1. Setup mínimo

`build.gradle.kts` (módulo app):

```kotlin
android {
    buildFeatures { compose = true }
}

dependencies {
    val composeBom = platform("androidx.compose:compose-bom:<version>")
    implementation(composeBom)
    implementation("androidx.compose.material3:material3")
    implementation("androidx.compose.ui:ui-tooling-preview")
    debugImplementation("androidx.compose.ui:ui-tooling")
    implementation("androidx.activity:activity-compose")
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose")
    implementation("androidx.lifecycle:lifecycle-runtime-compose")
    implementation("androidx.navigation:navigation-compose")
}
```

(Con Kotlin 2.0+ también se aplica el plugin `org.jetbrains.kotlin.plugin.compose`.)

`MainActivity`:

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            MiAppTheme {
                MiApp()
            }
        }
    }
}
```

## 2. Composables

Una función `@Composable` describe un trozo de UI. Nombre en **PascalCase**, devuelve `Unit`.

```kotlin
@Composable
fun Saludo(nombre: String, modifier: Modifier = Modifier) {
    Text(text = "Hola, $nombre", modifier = modifier)
}

@Preview(showBackground = true)
@Composable
fun SaludoPreview() {
    MiAppTheme { Saludo("Ana") }
}
```

Convenciones:
- Siempre acepta un `modifier: Modifier = Modifier` como primer parámetro opcional.
- Componibles pequeños y reutilizables.
- `@Preview` permite ver la UI en Android Studio sin ejecutar la app.

## 2.1 Componentes básicos (Material 3)

```kotlin
Text("Hola", style = MaterialTheme.typography.titleLarge)

Button(onClick = { /* acción */ }) { Text("Pulsar") }
OutlinedButton(onClick = {}) { Text("Secundario") }
TextButton(onClick = {}) { Text("Texto") }
IconButton(onClick = {}) { Icon(Icons.Default.Favorite, contentDescription = "Favorito") }

Image(
    painter = painterResource(R.drawable.logo),
    contentDescription = "Logo"
)
// Imágenes de red: librería Coil -> AsyncImage(model = url, contentDescription = null)

TextField(value = texto, onValueChange = { texto = it }, label = { Text("Nombre") })
OutlinedTextField(...)

Checkbox(checked = c, onCheckedChange = { c = it })
Switch(checked = s, onCheckedChange = { s = it })

Card { Text("Contenido", Modifier.padding(16.dp)) }
HorizontalDivider()
CircularProgressIndicator()
```

## 3. Layouts

| Composable | Función |
|---|---|
| `Column` | apila en vertical |
| `Row` | apila en horizontal |
| `Box` | apila uno encima de otro (z-order) |
| `LazyColumn` / `LazyRow` | listas con scroll eficientes (reciclan) |
| `LazyVerticalGrid` | cuadrícula |
| `Scaffold` | estructura de pantalla (topBar, bottomBar, FAB, contenido) |
| `Spacer` | espacio vacío |
| `ConstraintLayout` | posicionamiento por restricciones |

```kotlin
Column(
    modifier = Modifier.fillMaxSize().padding(16.dp),
    verticalArrangement = Arrangement.spacedBy(8.dp),
    horizontalAlignment = Alignment.CenterHorizontally
) {
    Text("Título")
    Row(verticalAlignment = Alignment.CenterVertically) {
        Icon(Icons.Default.Star, null)
        Spacer(Modifier.width(8.dp))
        Text("Destacado")
    }
}
```

`weight` reparte el espacio dentro de Row/Column:

```kotlin
Row { Box(Modifier.weight(1f)); Box(Modifier.weight(2f)) }
```

### Listas

```kotlin
LazyColumn(
    contentPadding = PaddingValues(16.dp),
    verticalArrangement = Arrangement.spacedBy(8.dp)
) {
    items(items = usuarios, key = { it.id }) { usuario ->   // key = estabilidad
        FilaUsuario(usuario)
    }
}
```

## 4. Modifier

Cadena de decoraciones/comportamiento. **El orden importa.**

```kotlin
Modifier
    .fillMaxWidth()          // ancho completo
    .height(56.dp)
    .padding(16.dp)          // padding después de background => entra dentro del color
    .background(Color.Red, RoundedCornerShape(8.dp))
    .clip(CircleShape)
    .border(1.dp, Color.Gray)
    .clickable { }
    .size(48.dp)
    .alpha(0.5f)
```

```kotlin
// Diferencia por orden:
Modifier.padding(16.dp).background(Color.Red)  // margen externo
Modifier.background(Color.Red).padding(16.dp)  // padding interno
```

Unidades: `dp` (tamaños), `sp` (texto).

## 5. Estado (el concepto central)

Compose se redibuja (**recomposición**) cuando cambia un `State`.

```kotlin
@Composable
fun Contador() {
    var cuenta by remember { mutableStateOf(0) }

    Button(onClick = { cuenta++ }) {
        Text("Pulsado $cuenta veces")
    }
}
```

- `mutableStateOf` => valor observable.
- `remember` => conserva el valor entre recomposiciones.
- `rememberSaveable` => además sobrevive a rotación / muerte de proceso.
- Sin `remember`, el estado se reinicia en cada recomposición.

### State hoisting (elevar el estado)

Hacer los composables **sin estado (stateless)**: reciben el valor y un callback; el estado vive más arriba.

```kotlin
// Stateless: reutilizable y testeable
@Composable
fun CampoNombre(valor: String, onCambio: (String) -> Unit) {
    TextField(value = valor, onValueChange = onCambio)
}

// Stateful: dueño del estado
@Composable
fun Formulario() {
    var nombre by rememberSaveable { mutableStateOf("") }
    CampoNombre(valor = nombre, onCambio = { nombre = it })
}
```

Patrón: **el estado baja, los eventos suben** (Unidirectional Data Flow).

### Efectos secundarios

```kotlin
LaunchedEffect(clave) {         // corrutina ligada al ciclo del composable; se relanza si cambia 'clave'
    viewModel.cargar()
}
DisposableEffect(clave) { onDispose { /* limpiar */ } }
val scope = rememberCoroutineScope()   // lanzar corrutinas desde eventos (onClick)
```

No hagas trabajo pesado ni llamadas de red directamente en el cuerpo de un composable: puede ejecutarse muchas veces.

## 6. Arquitectura de una Screen: ViewModel + UiState

Estructura recomendada (MVVM / UDF):

```
UI (Composable)  <--estado--  ViewModel  <--datos--  Repository  <--  API / DB
                 --eventos-->
```

### 6.1 Modelar el estado de la pantalla

```kotlin
data class ListaUiState(
    val cargando: Boolean = false,
    val usuarios: List<Usuario> = emptyList(),
    val error: String? = null
)
```

o con sealed interface:

```kotlin
sealed interface UiState {
    data object Cargando : UiState
    data class Exito(val usuarios: List<Usuario>) : UiState
    data class Error(val mensaje: String) : UiState
}
```

### 6.2 ViewModel

```kotlin
class ListaViewModel(
    private val repo: UsuarioRepository
) : ViewModel() {

    private val _uiState = MutableStateFlow<UiState>(UiState.Cargando)
    val uiState: StateFlow<UiState> = _uiState.asStateFlow()

    init { cargar() }

    fun cargar() {
        viewModelScope.launch {
            _uiState.value = UiState.Cargando
            _uiState.value = try {
                UiState.Exito(repo.obtenerUsuarios())
            } catch (e: Exception) {
                UiState.Error(e.message ?: "Error desconocido")
            }
        }
    }

    fun onUsuarioClick(id: Int) { /* ... */ }
}
```

- El `ViewModel` sobrevive a rotaciones y contiene la lógica de UI.
- Expón `StateFlow` inmutable; modifica solo con la variable privada.

### 6.3 Screen (conecta ViewModel con UI)

```kotlin
// Composable "con estado": conoce el ViewModel
@Composable
fun ListaScreen(
    viewModel: ListaViewModel = viewModel(),
    onNavegar: (Int) -> Unit
) {
    val state by viewModel.uiState.collectAsStateWithLifecycle()
    ListaContent(state, onReintentar = viewModel::cargar, onUsuarioClick = onNavegar)
}

// Composable "sin estado": solo pinta; fácil de previsualizar y testear
@Composable
fun ListaContent(
    state: UiState,
    onReintentar: () -> Unit,
    onUsuarioClick: (Int) -> Unit
) {
    when (state) {
        UiState.Cargando -> Box(Modifier.fillMaxSize(), Alignment.Center) {
            CircularProgressIndicator()
        }
        is UiState.Error -> Column(
            Modifier.fillMaxSize(),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            Text(state.mensaje)
            Button(onClick = onReintentar) { Text("Reintentar") }
        }
        is UiState.Exito -> LazyColumn {
            items(state.usuarios, key = { it.id }) { u ->
                ListItem(
                    headlineContent = { Text(u.nombre) },
                    modifier = Modifier.clickable { onUsuarioClick(u.id) }
                )
            }
        }
    }
}
```

> Usa `collectAsStateWithLifecycle()` (no `collectAsState`) para no recolectar cuando la app está en segundo plano.

## 7. Scaffold: estructura típica de pantalla

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun Pantalla() {
    Scaffold(
        topBar = { TopAppBar(title = { Text("Inicio") }) },
        bottomBar = { NavigationBar { /* items */ } },
        floatingActionButton = {
            FloatingActionButton(onClick = {}) { Icon(Icons.Default.Add, "Añadir") }
        }
    ) { innerPadding ->
        Column(Modifier.padding(innerPadding)) { /* contenido */ }
    }
}
```

Siempre aplica el `innerPadding` al contenido para que no quede tapado por las barras.

## 8. Navegación entre screens

Con **Navigation Compose** (versiones recientes soportan rutas tipadas con `@Serializable`).

```kotlin
// Rutas tipadas (plugin kotlinx-serialization)
@Serializable object Inicio
@Serializable data class Detalle(val id: Int)

@Composable
fun MiApp() {
    val navController = rememberNavController()

    NavHost(navController = navController, startDestination = Inicio) {
        composable<Inicio> {
            ListaScreen(onNavegar = { id -> navController.navigate(Detalle(id)) })
        }
        composable<Detalle> { backStackEntry ->
            val args = backStackEntry.toRoute<Detalle>()
            DetalleScreen(id = args.id, onVolver = { navController.popBackStack() })
        }
    }
}
```

Reglas:
- Pasa al `NavController` solo hacia las screens; los composables hijos reciben **callbacks** (`onVolver`, `onNavegar`) en vez del controller.
- Pasa **IDs**, no objetos completos; el destino carga los datos.
- Una instancia de `ViewModel` por destino con `viewModel()` o `hiltViewModel()`.

## 9. Tema (Material 3)

```kotlin
@Composable
fun MiAppTheme(
    darkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    MaterialTheme(
        colorScheme = if (darkTheme) darkColorScheme() else lightColorScheme(),
        typography = Typography(),
        content = content
    )
}

// Uso: no hardcodear colores ni fuentes
Text("Hola", color = MaterialTheme.colorScheme.primary,
     style = MaterialTheme.typography.headlineMedium)
```

Dynamic color (Android 12+): `dynamicLightColorScheme(context)` / `dynamicDarkColorScheme(context)`.

## 10. Recursos y buenas prácticas

- Strings en `res/values/strings.xml`: `stringResource(R.string.titulo)`.
- Imágenes: `painterResource(R.drawable.x)`; vectores: `Icons.Default.*` (dependencia `material-icons-extended` para más).
- **Accesibilidad**: `contentDescription` en iconos/imágenes, áreas táctiles ≥ 48dp.
- **Responsive**: `WindowSizeClass` para adaptar a teléfono/tablet/plegable.
- **Rendimiento**: usa `key` en `LazyColumn`, evita crear objetos pesados en el cuerpo del composable (`remember`), pasa estado estable/inmutable (`List` de data classes con `val`).
- **Testing**: `composeTestRule.setContent { ... }` + `onNodeWithText("...").performClick()`.
- Inyección de dependencias: **Hilt** o **Koin**.
- Red: **Retrofit** o **Ktor**; persistencia: **Room**, **DataStore**.

## 11. Animaciones rápidas

```kotlin
AnimatedVisibility(visible = visible) { Text("Aparezco") }

val color by animateColorAsState(if (activo) Color.Green else Color.Gray)
val tam by animateDpAsState(if (expandido) 200.dp else 100.dp)

Crossfade(targetState = pantalla) { p -> /* contenido según p */ }
```

---

# Resumen / Checklist para crear una screen

1. Definir el **`UiState`** (`data class` o `sealed interface`).
2. Crear el **`ViewModel`** que expone `StateFlow<UiState>` y funciones para eventos.
3. Crear `XScreen` (obtiene el ViewModel + recolecta estado) y `XContent` (UI sin estado).
4. Armar el layout con `Scaffold`, `Column`/`LazyColumn`, componentes Material 3 y `Modifier`.
5. Registrar la screen en el **`NavHost`**.
6. Añadir `@Preview` de `XContent` con datos de ejemplo.
7. Aplicar **tema**, strings y accesibilidad.

# Recursos

- Documentación oficial de Kotlin: https://kotlinlang.org/docs/home.html
- Kotlin Koans / Kotlin Playground: https://play.kotlinlang.org
- Jetpack Compose: https://developer.android.com/compose
- Curso gratuito Android Basics with Compose: https://developer.android.com/courses
