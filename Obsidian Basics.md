### 1. Formato básico (Markdown)

- **Títulos:** Usa `#` al inicio de la línea (`# H1`, `## H2`, `### H3`).
    
- **Énfasis:** `**negrita**`, `*cursiva*` o `~~tachado~~`.
    
- **Listas:** Usa `-` o `*` para viñetas; `1.` para listas numeradas.
    
- **Tareas (Checkboxes):** Escribe `- [ ] Tarea pendiente` y `- [x] Tarea hecha`.
    
- **Citas y bloques:** Usa `>` para citas textuales.
    
- **Bloques de código:** Usa tres tildes invertidas (```) arriba y abajo del código.´´´



### 2. Conexiones (el núcleo de Obsidian)

- **Enlaces internos (Wikilinks):** Escribe `[[Nombre de otra nota]]`. Si la nota no existe, hacer clic sobre el enlace la creará automáticamente.
    
- **Alias de enlace:** `[[Nombre de la nota|Texto visible alternativo]]`.
    
- **Enlazar a encabezados o bloques:** `[[Nombre de la nota#Encabezado]]` o `[[Nombre de la nota^bloque]]`.
    
- **Incrustar contenido:** Agrega un signo de exclamación al inicio (`![[Nota o imagen]]`) para previsualizar una imagen o el contenido completo de otra nota dentro de la actual.
    

### 3. Organización y metadatos

- **Etiquetas (Tags):** Usa `#etiqueta` o jerárquicas como `#proyecto/fase1`.
    
- **Propiedades (Frontmatter):** Agrega metadatos estructurados al inicio del archivo abriendo y cerrando con tres guiones (`---`):
    
    YAML
    
    ```
    ---
    fecha: 2026-10-06
    tipo: reunión
    tags: [trabajo, idea]
    ---
    ```
    

### Atajos útiles para empezar

- `Ctrl + N` (o `Cmd + N`): Crear nueva nota.
    
- `Ctrl + O` (o `Cmd + O`): Buscador rápido para abrir cualquier archivo al instante.
    
- `Ctrl + E` (o `Cmd + E`): Alternar entre el modo de edición y lectura.