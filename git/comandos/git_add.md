🎯 Comando #2: git add - Preparando Cambios

📦 El problema del "limbo de archivos":

```text
Tienes archivos modificados pero...
❌ No están listos para commit
❌ Git no sabe qué cambios incluir
❌ No puedes decidir qué guardar
```

✨ La solución organizada:

```bash
# Preparar archivos específicos
git add archivo.html

# Preparar TODOS los cambios
git add .

# Preparar solo ciertos tipos
git add *.js
```

🧠 ¿Qué significa realmente git add?

Imagina que Git tiene 3 áreas:

```text
Área de Trabajo     →     Área de Staging     →     Repositorio
 (Working Dir)            (Staging Area)           (.git/)
     ↓                         ↓                        ↓
Trabajas aquí         Preparas aquí           Guardas permanentemente
 Archivos nuevos      Seleccionas qué         Commits históricos
 Modificaciones       cambios incluir         Versiones finales
```

**Con git add:** Mueves archivos del Área de Trabajo al Área de Staging

🧪 Ejemplos prácticos:

```bash
# Situación: Tienes varios archivos modificados
git status

# Verás algo como:
# Changes not staged for commit:
#   modified:   index.html
#   modified:   styles.css
#   new file:   script.js
#   deleted:    old-file.txt

# 1. Añadir solo UN archivo
git add index.html

# 2. Añadir todos los archivos .css
git add *.css

# 3. Añadir todo en la carpeta actual
git add .

# 4. Añadir interactivamente (te pregunta uno por uno)
git add -p
```

🎮 Modos de uso de git add:

| Comando | ¿Qué hace? | ¿Cuándo usarlo? |
|---------|-----------|-----------------|
| `git add archivo` | Añade un archivo específico | Cambios importantes que quieres commitear |
| `git add .` | Añade TODO en la carpeta actual | Muchos cambios relacionados |
| `git add -A` | Añade TODO (incluyendo borrados) | Limpieza completa del proyecto |
| `git add *.js` | Añade solo archivos JavaScript | Cambios específicos de tipo |
| `git add -p` | Añade interactivamente (patch) | Quieres revisar cada cambio antes |
| `git add carpeta/` | Añade toda una carpeta | Reestructuración de directorios |

💡 Consejos profesionales:

**1. El poder de git add -p (modo patch):**

```bash
# Git te muestra cada cambio y pregunta:
Stage this hunk [y,n,q,a,d,s,e,?]?

# Opciones:
y → Sí, añadir este fragmento
n → No, no añadir
q → Salir
s → Dividir en fragmentos más pequeños
e → Editar manualmente
? → Ver ayuda
```

**2. Ignorar archivos temporalmente:**

```bash
# Añadir todo EXCEPTO un archivo
git add .
git reset archivo-no-deseado.txt

# O usando .gitignore temporal
echo "archivo-temporal.log" >> .gitignore
git add .
```

🚨 Errores comunes:

**❌ Problema: Añadí archivos que no quería**

```bash
# Deshacer el add de un archivo específico
git reset archivo-mal.html

# Deshacer TODO lo añadido
git reset

# Verificar que se deshizo
git status
```

**❌ Problema: Archivos demasiado grandes**

```bash
# Error: fatal: unable to stat 'video.mp4': File too large

# Solución 1: Añadir al .gitignore
echo "*.mp4" >> .gitignore

# Solución 2: Usar Git LFS (Large File Storage)
git lfs track "*.mp4"
git add .gitattributes
git add video.mp4
```

🌍 Flujo de trabajo real:

**Escenario: Desarrollando una feature nueva**

```bash
# 1. Trabajas en varios archivos
vim header.html
vim styles.css
vim main.js

# 2. Ver qué has cambiado
git status
git diff  # Ver diferencias

# 3. Decidir qué incluir
# Solo quiero commitear header.html y styles.css por ahora
git add header.html styles.css

# 4. Verificar qué está preparado
git status  # Ahora muestra "Changes to be committed"

# 5. main.js sigue en "Changes not staged"
# Lo terminaré y commitearé después
```

📊 Tabla: Estados de los archivos en Git

| Estado | Descripción | Comandos útiles |
|--------|-------------|-----------------|
| Untracked | Nuevo archivo, Git no lo conoce | `git add` para empezar a rastrear |
| Modified | Archivo modificado pero no preparado | `git diff` para ver cambios |
| Staged | Preparado para commit | `git commit` para guardar |
| Committed | Guardado en el historial | `git log` para ver historia |
| Ignored | Git lo ignora completamente | Listado en `.gitignore` |

🎯 Ejercicio práctico:

**Tu tarea: Aprender a usar git add selectivamente**

```bash
# 1. Crear varios archivos
echo "HTML" > index.html
echo "CSS" > style.css
echo "JS" > app.js
echo "TEMP" > temp.log

# 2. Ver estado inicial
git status

# 3. Añadir solo los archivos de código
git add *.html *.css *.js

# 4. Ver qué pasó
git status  # temp.log debería seguir como "untracked"

# 5. Probar modo interactivo
# Primero, modifica un archivo
echo "/* Más CSS */" >> style.css
git add -p  # Te preguntará sobre cada cambio
```

🔧 Configuraciones útiles:

```bash
# Mostrar archivos ignorados en git status
git config --global status.showUntrackedFiles all

# Alias para comandos comunes
git config --global alias.s "status"
git config --global alias.a "add"
git config --global alias.ap "add -p"

# Ahora puedes usar:
git s  # en lugar de git status
git a .  # en lugar de git add .
git ap  # en lugar de git add -p
```

💭 Preguntas frecuentes:

**❓ ¿Cuál es la diferencia entre git add . y git add -A?**

```bash
# En la carpeta raíz: Son iguales
# En subcarpetas:
git add .      # Añade todo en la CARPETA ACTUAL y subcarpetas
git add -A     # Añade TODO en TODO el repositorio

# Ejemplo: Estás en carpeta/src/
git add .      # Solo añade en src/
git add -A     # Añade en todo el proyecto
```

**❓ ¿Puedo deshacer un git add después de commitear?**

```bash
# Sí, pero necesitas más pasos:
# 1. Deshacer el commit (pero mantener cambios)
git reset --soft HEAD~1

# 2. Ahora puedes deshacer el add
git reset archivo-no-deseado.txt

# 3. Hacer nuevo commit con lo correcto
git commit -m "Mensaje corregido"
```

🎨 Visualizando el proceso:

```
graph LR
    A[Trabajas en<br>archivos] --> B{git status<br>ver estado}
    B --> C[Archivos modificados]
    C --> D{git add<br>seleccionar cambios}
    D --> E[Área de Staging]
    E --> F[git commit<br>guardar]
    F --> G[Historial Git]
    
    style A fill:#e1f5fe
    style E fill:#f3e5f5
    style G fill:#e8f5e8
```

<div align="center">

**🎯 Punto Clave de git add:**

```diff
+ Es el SELECTOR de cambios para commits
+ Te permite organizar tus commits lógicamente
+ Puedes añadir cambios parciales de archivos
+ Sin esto, no puedes hacer commits organizados
```

</div>

