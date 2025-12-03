🎯 Comando #6: git branch - Trabajo Paralelo

🌳 El problema del "camino único":

```text
Trabajas en un proyecto...
❌ Quieres probar una idea radical (pero no romper lo que funciona)
❌ Necesitas arreglar un bug urgente (mientras desarrollas una feature)
❌ Tu colega quiere trabajar en otra cosa (al mismo tiempo)
❌ No puedes tener múltiples versiones del código
```

🌿 La solución de los "universos paralelos":

```bash
# Crear una nueva rama
git branch nueva-feature

# Ver todas las ramas
git branch
```

**Salida típica:**

```text
  feature/login
  feature/search
* main              ← Estás AQUÍ
  develop
  hotfix/urgente
```

🧠 ¿Qué es una rama realmente?

Imagina ramas como:

```text
🌳 **Ramas de un árbol** - Todas vienen del tronco, pero crecen en direcciones diferentes
🎬 **Líneas de tiempo alternativas** - "¿Qué pasaría si...?" versiones de tu código
🧪 **Laboratorios experimentales** - Lugares seguros para probar cosas nuevas
🚧 **Áreas de construcción** - Donde se construyen features sin molestar el tráfico principal
```

**Técnicamente:** Una rama es solo un puntero móvil a un commit.

🧪 Ejemplos prácticos:

```bash
# 1. Ver ramas locales
git branch

# 2. Ver ramas locales Y remotas
git branch -a
# * main
#   remotes/origin/main
#   remotes/origin/develop

# 3. Crear rama nueva
git branch nueva-feature

# 4. Crear rama y cambiar a ella (combo)
git checkout -b feature/login

# 5. Renombrar rama actual
git branch -m nuevo-nombre

# 6. Eliminar rama (si ya está fusionada)
git branch -d feature-vieja

# 7. Eliminar rama (FORZAR, aunque no esté fusionada)
git branch -D feature-rota

# 8. Ver ramas no fusionadas
git branch --no-merged

# 9. Ver ramas ya fusionadas
git branch --merged
```

📊 Flujo de trabajo con ramas:

**Git Flow (Popular para proyectos)**

```text
main (producción)
  ↑
release/ (pre-producción)
  ↑
develop (desarrollo principal)
  ↑
feature/ (nuevas funcionalidades)
```

**GitHub Flow (Más simple)**

```text
main (siempre desplegable)
  ↑
feature/ (cualquier cambio)
```

**Tu propio flujo**

```bash
# 1. Rama principal (estable)
main

# 2. Rama para cada tarea
feature/navbar-responsive
bugfix/login-error
hotfix/security-patch
docs/update-readme
refactor/auth-system
```

🌍 Caso real: Empresa de e-commerce

**Situación: Black Friday se acerca...**

```bash
# Rama principal (producción)
git checkout main

# 1. Bug crítico en checkout (URGENTE)
git checkout -b hotfix/checkout-bug
# Arreglas bug, pruebas, mergeas a main
# ✅ Clientes felices

# 2. Nueva feature: Cupones de descuento
git checkout -b feature/cupones
# Desarrollas por 2 semanas
# Cuando terminas, mergeas a main
# ✅ Nueva funcionalidad lista

# 3. Refactorización del carrito
git checkout -b refactor/carrito
# Trabajas 1 semana, pero encuentras problemas
# Decides abandonar la refactorización por ahora
git checkout main
git branch -D refactor/carrito
# ❌ Sin daños al código principal

# TODAS estas tareas en PARALELO, sin conflictos 🎉
```

🎯 Nomenclatura recomendada:

```bash
# Tipos comunes de ramas:
feature/    # Nueva funcionalidad
bugfix/     # Corrección de error
hotfix/     # Corrección URGENTE en producción
release/    # Preparar nueva versión
docs/       # Documentación
test/       # Pruebas
chore/      # Tareas de mantenimiento
refactor/   # Reestructurar código

# Ejemplos buenos:
feature/user-profile
bugfix/login-validation
hotfix/payment-gateway
release/v2.0.0
docs/api-reference
test/unit-tests-auth
chore/update-dependencies
refactor/database-layer
```

💡 Crear ramas desde diferentes puntos:

```bash
# 1. Desde HEAD (donde estás ahora)
git branch nueva-desde-aqui

# 2. Desde otra rama
git branch nueva-desde-develop develop

# 3. Desde un tag específico
git branch desde-tag v1.2.3

# 4. Desde un commit específico
git branch desde-commit abc123def

# 5. Desde hace N commits atrás
git branch desde-hace-5 HEAD~5
```

🚨 Errores comunes:

**❌ Error 1: Ramas sin sentido**

```bash
# MAL: 
git branch "trabajo-del-miercoles"
git branch "prueba"
git branch "cambios"

# BIEN:
git branch "feature/dark-mode"
git branch "bugfix/scroll-mobile"
git branch "docs/installation-guide"
```

**❌ Error 2: Demasiadas ramas activas**

```bash
# Síntoma: 20 ramas locales, no sabes cuál es cuál
# Solución: Limpieza mensual

# Ver ramas fusionadas (se pueden borrar)
git branch --merged main
# feature/login
# bugfix/navbar
# docs/update

# Eliminar ramas fusionadas
git branch --merged main | grep -v "\*" | xargs -n 1 git branch -d
```

**❌ Error 3: Rama local sin remota**

```bash
# Creaste rama local, pero olvidaste subirla
git push -u origin feature/nueva
# -u establece upstream (relación local-remota)
```

🔍 Inspeccionar ramas:

```bash
# 1. Ver última commit en cada rama
git branch -v
# main       abc1234 feat: nueva funcionalidad
# develop    def5678 fix: bug crítico

# 2. Ver ramas que contienen un commit
git branch --contains abc123

# 3. Ver ramas por última actividad
git for-each-ref --sort=-committerdate refs/heads/ --format='%(refname:short) %(committerdate:relative)'

# 4. Comparar ramas
git log main..feature/nueva  # commits en feature que main no tiene
git log feature/nueva..main  # commits en main que feature no tiene

# 5. Ver diferencias entre ramas
git diff main..feature/nueva  # cambios entre ramas
```

🎮 Mini-juego: ¿Qué rama crear?

| Situación | Tipo de rama | Nombre sugerido |
|-----------|-------------|-----------------|
| Agregar login con Google | feature/ | feature/google-auth |
| Error en cálculo de precios | bugfix/ | bugfix/price-calculation |
| Actualizar documentación API | docs/ | docs/api-update |
| Agregar pruebas unitarias | test/ | test/unit-tests |
| Seguridad urgente en login | hotfix/ | hotfix/login-security |
| Migrar a nueva versión de React | chore/ | chore/react-migration |

🔧 Configuraciones útiles:

```bash
# 1. Auto-completado para nombres de ramas
git config --global bash.completion true

# 2. Mostrar rama en prompt
export PS1='\u@\h:\w$(__git_ps1 " (%s)")\$ '

# 3. Configurar merge behavior
git config --global pull.rebase true  # Para ramas más limpias

# 4. Alias útiles
git config --global alias.br "branch"
git config --global alias.co "checkout"
git config --global alias.cb "checkout -b"  # crear y cambiar

# 5. Establecer rama por defecto para push
git config --global push.default current
```

🌈 Ramas remotas vs locales:

```bash
# RAMAS LOCALES (en tu computadora)
git branch
# * main
#   feature/login
#   develop

# RAMAS REMOTAS (en GitHub/GitLab)
git branch -r
# origin/main
# origin/develop
# origin/feature/login

# TODAS LAS RAMAS
git branch -a
# * main
#   feature/login
#   remotes/origin/main
#   remotes/origin/develop

# Sincronizar ramas remotas
git fetch  # Trae información de ramas remotas
git checkout -b nueva-local origin/nueva-remota  # Crear local desde remota
```

🎯 Ejercicio práctico:

**Tu misión: Gestionar un proyecto con múltiples ramas**

```bash
# 1. Crear proyecto
mkdir proyecto-ramas
cd proyecto-ramas
git init
echo "# Proyecto" > README.md
git add . && git commit -m "Initial commit"

# 2. Crear estructura de ramas
git checkout -b develop
echo "// código desarrollo" > app.js
git add . && git commit -m "Setup desarrollo"

# 3. Trabajar en features paralelas
git checkout -b feature/navbar
echo "// navbar código" >> app.js
git add . && git commit -m "Add navbar"

git checkout develop
git checkout -b feature/footer
echo "// footer código" >> app.js
git add . && git commit -m "Add footer"

# 4. Ver estado
git branch -a --list
git log --oneline --graph --all

# 5. Limpiar ramas terminadas
# (Supongamos que navbar ya fue mergeado)
git checkout develop
git merge feature/navbar
git branch -d feature/navbar
```

💭 Preguntas frecuentes:

**❓ ¿Cuántas ramas debería tener?**

```text
✅ BUENO: 3-5 ramas activas por persona
❌ MAL: 20+ ramas olvidadas

Regla: Una rama por "tarea lógica" que:
• Puede desarrollarse independientemente
• Tiene un propósito claro
• Se puede probar/mergear por separado
```

**❓ ¿Ramas largas vs cortas?**

```bash
# RAMAS CORTAS (recomendado)
# • Pocos días de trabajo
# • Pocos commits (5-10)
# • Fáciles de review
# • Menos conflictos de merge

# RAMAS LARGAS (evitar)
# • Semanas/meses de trabajo
# • Decenas de commits
# • Difíciles de review
# • Conflictos enormes
```

**❓ ¿Qué pasa si borro una rama por error?**

```bash
# ¡Tranquilo! Los commits NO se pierden.
# 1. Encontrar el último commit de la rama
git reflog | grep "feature/perdida"

# 2. Recuperar la rama
git branch feature/perdida abc123  # abc123 es el hash del commit

# Los commits siguen ahí por ~30 días
# hasta que Git hace garbage collection
```

📊 Tabla de comandos branch:

| Comando | Descripción | Uso común |
|---------|------------|-----------|
| `git branch` | Listar ramas locales | Ver dónde estás |
| `git branch -a` | Listar TODAS las ramas | Ver estructura completa |
| `git branch nombre` | Crear rama nueva | Empezar nueva tarea |
| `git branch -d nombre` | Eliminar rama fusionada | Limpieza |
| `git branch -D nombre` | Eliminar rama (forzar) | Descartar trabajo |
| `git branch -m nuevo` | Renombrar rama actual | Corregir nombre |
| `git branch -vv` | Ver ramas con tracking | Ver relaciones |
| `git branch --merged` | Ver ramas fusionadas | Limpieza |
| `git branch --no-merged` | Ver ramas no fusionadas | Pendientes |

🎨 Visualizando las ramas:

```
gitGraph
    commit id: "initial"
    branch develop
    checkout develop
    commit id: "setup"
    branch feature/navbar
    checkout feature/navbar
    commit id: "navbar v1"
    commit id: "navbar v2"
    checkout develop
    branch feature/footer
    checkout feature/footer
    commit id: "footer v1"
    checkout develop
    merge feature/navbar id: "merge navbar"
    commit id: "update"
    merge feature/footer id: "merge footer"
    checkout main
    merge develop id: "release"
```

<div align="center">

**🎯 Punto Clave de git branch:**

```diff
+ Permite trabajar en MÚLTIPLES cosas a la vez
+ Aísla cambios experimentales del código estable
+ Facilita colaboración en equipo
+ Sin ramas, Git sería solo un historial lineal
```

</div>

