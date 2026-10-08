## 📂 1. Archivos y Explorador

| **Comando**         | **Acción**                                                      |
| ------------------- | --------------------------------------------------------------- |
| `Space` + `e`       | Abrir/Cerrar el explorador de archivos lateral (Neo-tree).      |
| `Space` + `Space`   | Buscar cualquier archivo por nombre en el proyecto.             |
| `Space` + `f` + `r` | Mostrar archivos recientes.                                     |
| `Space` + `s` + `g` | Buscar una palabra/texto en **todos** los archivos (Live Grep). |

## 🗂️ 2. Navegación (Pestañas y Pantallas)

_En Vim, las pestañas abiertas se llaman "Buffers"._

|**Comando**|**Acción**|
|---|---|
|`Shift` + `h`|Ir a la pestaña (buffer) anterior (Izquierda).|
|`Shift` + `l`|Ir a la pestaña (buffer) siguiente (Derecha).|
|`Space` + `b` + `d`|Cerrar la pestaña actual (_Buffer Delete_).|
|`Space` + `w` + `v`|Dividir la pantalla verticalmente.|
|`Ctrl` + `h/j/k/l`|Mover el cursor entre las pantallas divididas.|

## 💻 3. Código y C++ (LSP)

_Ideal para tu código de OpenMP y CUDA. LazyVim detecta errores y autocompleta usando `clangd`._

|**Comando**|**Acción**|
|---|---|
|`g` + `d`|Ir a la definición de una función o variable (_Go to Definition_).|
|`K` (Mayúscula)|Mostrar documentación de la función bajo el cursor (Hover).|
|`Space` + `c` + `r`|Renombrar una variable en todos lados (_Code Rename_).|
|`Space` + `c` + `a`|Sugerencias para arreglar errores (_Code Action_).|
|`Space` + `x` + `x`|Abrir panel inferior con todos los errores del archivo.|

## 🛠️ 4. Utilidades Prácticas

|**Comando**|**Acción**|
|---|---|
|`Ctrl` + `/`|Abrir/Ocultar una **Terminal flotante** (¡Perfecto para compilar con `g++`!).|
|`Space` + `l`|Abrir el gestor de plugins (Lazy).|
|`Space` + `c` + `m`|Abrir Mason (Para instalar formateadores o servidores extra).|

## 🧭 5. Supervivencia Vim (Por si acaso)

|**Comando**|**Acción**|
|---|---|
|`i`|Modo Insertar (Para empezar a escribir código).|
|`Esc`|Salir del modo de escritura (Volver al modo normal).|
|`:w` + `Enter`|Guardar archivo (_Write_).|
|`:q` + `Enter`|Salir (_Quit_).|
|`u`|Deshacer el último cambio (_Undo_).|
|`Ctrl` + `r`|Rehacer el cambio (_Redo_).|
