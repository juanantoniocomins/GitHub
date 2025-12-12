# 🎯 Comando #4: git status - El Dashboard de Git

📊 El problema de la "ceguera":

```text
Trabajas en varios archivos...
❌ ¿Qué archivos he modificado?
❌ ¿Qué está listo para commit?
❌ ¿Hay archivos nuevos?
❌ ¿He borrado algo sin querer?
```

👁️ La solución de "visión completa":

```bash
# Ver TODO el estado actual
git status
```

**Salida típica:**

```text
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html        ← VERDE: Listo para commit

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   styles.css        ← ROJO: Modificado pero no preparado

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        nuevo-archivo.js              ← ROJO: Nuevo, Git no lo conoce
```

🎨 Modos de visualización:

```bash
# 1. Estado normal (default)
git status

# 2. Estado corto (máquina readable)
git status --short
# Salida: M  index.html    (M = Modified)
#        A  nuevo.txt      (A = Added)
#        D  viejo.txt      (D = Deleted)
#        ?? sin-seguir.js  (?? = Untracked)

# 3. Estado con ramas
git status -b
# On branch main
# Your branch is ahead of 'origin/main' by 2 commits.

# 4. Mostrar archivos ignorados también
git status --ignored
```

📊 Tabla de códigos --short:

| Código | Significado | Área |
|--------|------------|------|
| M | Modificado (not staged) | Working Directory |
| M | Modificado (staged) | Staging Area |
| MM | Modificado en ambas | WD y Staging |
| A | Añadido (nuevo) | Staging Area |
| D | Borrado (not staged) | Working Directory |
| D | Borrado (staged) | Staging Area |
| R | Renombrado | Staging Area |
| C | Copiado | Staging Area |
| ?? | Sin seguimiento | Untracked |
| !! | Ignorado | .gitignore |

🧪 Ejemplos prácticos:

**Escenario 1: Recién empiezas a trabajar**

```bash
git status
# On branch main
# nothing to commit, working tree clean
# ✅ Todo está limpio y guardado
```

**Escenario 2: Después de modificar archivos**

```bash
# Editas varios archivos...
vim app.js
vim styles.css
touch nuevo.html

git status
# Changes not staged for commit: app.js, styles.css
# Untracked files: nuevo.html
# ⚠️ Tienes trabajo pendiente
```

**Escenario 3: Después de git add**

```bash
git add app.js
git status
# Changes to be committed: app.js
# Changes not staged for commit: styles.css  
# Untracked files: nuevo.html
# 🎯 app.js está listo para commit
```

🔍 Ver diferencias específicas:

```bash
# Ver QUÉ cambió en archivos no preparados
git diff

# Ver QUÉ cambió en archivos ya preparados
git diff --staged

# Ver cambios en un archivo específico
git diff styles.css

# Ver estadísticas de cambios
git diff --stat
# styles.css | 10 +++++-----
# app.js     |  5 +++++
# 2 files changed, 10 insertions(+), 5 deletions(-)
```

🚨 Estados problemáticos y soluciones:

**Problema 1: Muchos archivos modificados (abrumador)**

```bash
# Usa --short para ver solo lo esencial
git status --short

# O agrupa por estado
git status | grep -A5 "Changes to be committed"
git status | grep -A5 "Changes not staged"
```

**Problema 2: Archivos que no deberían estar ahí**

```bash
# Ver qué archivos están siendo rastreados
git ls-files

# Si hay archivos grandes o temporales
echo "*.log" >> .gitignore
echo "node_modules/" >> .gitignore
git rm --cached archivo-grande.mp4
```

**Problema 3: Estado confuso después de merge**

```bash
# Ver conflictos pendientes
git status
# Both modified: archivo-conflicto.js

# Resolver conflictos, luego:
git add archivo-conflicto.js
git status  # Ya no debería mostrar conflictos
```

🌍 Flujo de trabajo real:

**Desarrollador trabajando en feature:**

```bash
# Mañana: Empieza a trabajar
git status  # Todo limpio

# Edita algunos archivos
vim src/components/Header.js
vim src/styles/main.css

# Antes de almuerzo: Revisa progreso
git status
# Changes not staged: Header.js, main.css
# ⏰ Buen momento para hacer commit parcial

git add src/components/Header.js
git commit -m "feat: mejorar navegación responsive"

git status
# Cambios pendientes: solo main.css
# ✅ Progreso guardado, puedo continuar después
```

💡 Trucos profesionales:

```bash
# 1. Alias para status corto
git config --global alias.s "status --short"

# Ahora usa: git s

# 2. Colores personalizados
git config --global color.status.added "green"
git config --global color.status.changed "yellow"
git config --global color.status.untracked "red"

# 3. Ver estado ignorando whitespace
git diff --word-diff  # Útil para cambios de formato

# 4. Estado antes/después de comandos
git status  # Antes
git add .
git status  # Después - ve la diferencia
```

🎯 Ejercicio práctico:

**Tu misión: Dominar el flujo de estados Git**

```bash
# 1. Crear proyecto de práctica
mkdir practica-status
cd practica-status
git init

# 2. Crear archivos en diferentes estados
echo "v1" > modificado.txt
echo "nuevo" > sin-seguir.txt
git add modificado.txt
git commit -m "commit inicial"

# 3. Cambiar archivos existentes
echo "v2" > modificado.txt
echo "para-borrar" > borrar.txt
git add borrar.txt
git commit -m "agregar borrar.txt"

# 4. Ver diferentes estados
rm borrar.txt                 # Borrar archivo rastreado
echo "ignorar" > temporal.log # Crear archivo que ignoraremos
echo "*.log" > .gitignore     # Configurar ignore

# 5. Ver todos los estados
git status
git status --short
git status --ignored
```

**Deberías ver:**

- **modificado.txt**: Changes not staged
- **borrar.txt**: Changes not staged (deleted)
- **temporal.log**: Ignored (por .gitignore)
- **sin-seguir.txt**: Untracked files

🔧 Configuraciones útiles:

```bash
# Mostrar rama siempre en prompt
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$(__git_ps1 " (%s)")\$ '

# O usar Git Bash en Windows que ya lo incluye

# Configurar editor para mensajes largos
git config --global core.editor "code --wait"

# Habilitar autocompletado
# En bash: 
source /usr/share/bash-completion/completions/git

# En zsh:
autoload -Uz compinit && compinit
```

💭 Preguntas frecuentes:

**❓ ¿Por qué git status muestra archivos que no modifiqué?**

```bash
# Posibles razones:
# 1. Cambios de permisos: chmod +x script.sh
# 2. Cambios de línea fin de línea (CRLF vs LF)
# 3. Espacios en blanco al final
# 4. Timestamps cambiaron pero no contenido

# Ver cambios exactos:
git diff --no-ext-diff archivo.confuso.js
```

**❓ ¿Cómo saber qué archivos están listos para push?**

```bash
# Ver commits locales no enviados
git status -b
# Your branch is ahead of 'origin/main' by 2 commits.

# O más específico:
git log --oneline origin/main..HEAD
# Muestra commits locales que el remoto no tiene
```

**❓ ¿git status es lento en proyectos grandes?**

```bash
# Sí, puede serlo. Soluciones:

# 1. Usar --short (más rápido)
git status --short

# 2. Limitar a cierta profundidad
git status src/  # Solo carpeta src

# 3. Usar herramientas gráficas para proyectos grandes
# Como GitKraken, Sourcetree, o el VS Code Git integration
```

🎨 Visualizando el flujo:

```
graph TD
    A[Trabajas<br>en archivos] --> B{git status}
    B --> C[Verde: staged]
    B --> D[Rojo: not staged]
    B --> E[Rojo: untracked]
    C --> F[git commit]
    D --> G[git add]
    E --> H[git add o .gitignore]
    G --> C
    F --> I[Historial seguro]
    
    style C fill:#e8f5e8
    style D fill:#ffebee
    style E fill:#ffebee
    style I fill:#f3e5f5
```

📊 Resumen de comandos relacionados:

| Comando | Para qué sirve | Relación con git status |
|---------|---------------|------------------------|
| `git diff` | Ver cambios específicos | Complementa status mostrando QUÉ cambió |
| `git add` | Preparar cambios | Convierte rojo → verde en status |
| `git reset` | Deshacer add | Convierte verde → rojo en status |
| `git clean` | Limpiar untracked | Elimina archivos rojos (untracked) |
| `git stash` | Guardar temporal | Limpia status temporalmente |
| `git commit` | Guardar cambios | Limpia área verde |

<div align="center">

**🎯 Punto Clave de git status:**

```diff
+ Es tu "dashboard" de Git
+ Te muestra EXACTAMENTE dónde estás
+ Ayuda a tomar decisiones (add, commit, ignore)
+ Sin esto, trabajas "a ciegas"
```

</div>

