🎯 Comando #7: git checkout - Navegación Inteligente

🧭 El problema del "estancamiento":

```text
Tienes múltiples ramas pero...
❌ ¿Cómo cambio de rama?
❌ ¿Cómo veo cómo estaba el código ayer?
❌ ¿Cómo pruebo un commit antiguo?
❌ ¿Cómo descarto cambios no deseados?
```

🚀 La solución del "teletransporte Git":

```bash
# Cambiar a otra rama
git checkout otra-rama

# Crear y cambiar a nueva rama
git checkout -b nueva-rama

# Ver cómo estaba un archivo en commit antiguo
git checkout abc123 -- archivo.js
```

🎭 Los 3 usos principales:

**1. Cambiar entre ramas**

```bash
# Ir a rama existente
git checkout develop
git checkout feature/login
git checkout main

# Verificar que cambió
git branch
# * develop    ← Ahora estás AQUÍ
#   feature/login
#   main
```

**2. Crear nueva rama y cambiar**

```bash
# Combo mágico: crear Y cambiar
git checkout -b feature/dark-mode
# Equivale a:
git branch feature/dark-mode
git checkout feature/dark-mode
```

**3. Recuperar archivos antiguos**

```bash
# Recuperar archivo de commit específico
git checkout abc123 -- config.js

# Recuperar archivo de otra rama
git checkout develop -- database.sql

# Descartar cambios locales no deseados
git checkout -- archivo-roto.js
```

🧪 Ejemplos prácticos:

**Escenario 1: Cambio rápido entre tareas**

```bash
# Estás en feature/login, pero surge bug urgente
git stash                    # Guarda cambios temporales
git checkout main            # Vas a producción
git checkout -b hotfix/bug   # Creas rama para bug
# Arreglas bug, commit, merge
git checkout feature/login   # Vuelves a tu trabajo
git stash pop                # Recuperas cambios
```

**Escenario 2: Recuperar archivo borrado**

```bash
# Borraste archivo importante por error
rm config-importante.js

# Recuperar de Git
git checkout HEAD -- config-importante.js
# ¡Archivo recuperado!
```

**Escenario 3: Probar código antiguo**

```bash
# Quieres ver cómo funcionaba hace 1 mes
git log --oneline --since="1 month ago"
# abc123 feat: nueva UI
# def456 fix: bug login

# Viajar en el tiempo
git checkout abc123
# Ahora estás en modo "detached HEAD"
# Puedes probar, pero no hacer commits

# Para volver al presente
git checkout main
```

⚠️ Modo "Detached HEAD" (Cabeza desprendida):

```bash
# Esto te pone en detached HEAD:
git checkout abc123        # Hash de commit
git checkout HEAD~3        # 3 commits atrás
git checkout v1.2.3        # Tag

# ¿Qué significa?
# • No estás en una rama
# • Puedes ver código viejo
# • Si haces commits, se perderán (a menos que crees rama)

# Solución si quieres guardar cambios:
git checkout -b experimento  # Crea rama desde aquí
```

💡 Trucos avanzados:

**1. Navegación relativa:**

```bash
git checkout HEAD~1    # 1 commit atrás
git checkout HEAD~3    # 3 commits atrás  
git checkout HEAD^     # Commit padre
git checkout HEAD^^    # Abuelo
git checkout HEAD~2^   # Bisabuelo (2 atrás, luego padre)
```

**2. Checkout de múltiples archivos:**

```bash
# Recuperar varios archivos de otra rama
git checkout develop -- src/ utils/ config/

# Usar patrones
git checkout develop -- "*.js" "*.css"
```

**3. Checkout interactivo:**

```bash
# Ver qué cambiaría sin hacerlo realmente
git checkout --patch otra-rama
# Te pregunta por cada cambio
```

**4. Crear rama desde tag:**

```bash
git checkout -b version-2.0 v2.0.0
# Crea rama desde el tag v2.0.0
```

🚨 Errores comunes y soluciones:

**❌ Error: "Your local changes would be overwritten"**

```bash
# Tienes cambios no commitados y quieres cambiar de rama
# Opciones:
git stash                    # Guardar cambios temporalmente
git checkout otra-rama
# Luego: git stash pop

git commit -m "WIP"          # Commit temporal
git checkout otra-rama

git checkout -f otra-rama    # FORZAR (pierdes cambios)
```

**❌ Error: "Already on 'branch-name'"**

```bash
# Ya estás en esa rama, no hay nada que cambiar
# Verifica dónde estás:
git branch
```

**❌ Error: "pathspec did not match any files"**

```bash
# El archivo no existe en ese commit/rama
# Verifica nombres:
git ls-tree -r otra-rama --name-only | grep archivo
```

🌍 Flujo de trabajo real:

**Desarrollador full-stack trabajando en múltiples features:**

```bash
# Lunes mañana: Empezar feature frontend
git checkout main
git checkout -b feature/dark-mode-frontend
# Trabajo en CSS, JavaScript...

# Martes: Bug crítico en backend (URGENTE)
git stash
git checkout main
git checkout -b hotfix/api-crash
# Arreglo bug, pruebas, merge a main
git push

# Miércoles: Volver a frontend
git checkout feature/dark-mode-frontend
git stash pop
# Continuar donde dejé

# Jueves: Feature necesita cambios en backend también
git checkout main
git checkout -b feature/dark-mode-backend
# Trabajo en API endpoints

# Viernes: Unir ambos features
git checkout feature/dark-mode-frontend
git merge feature/dark-mode-backend
# Resuelvo conflictos, pruebo completo
```

🔍 Checkout vs Restore vs Switch:

**Git moderno (2.23+) separó funciones:**

```bash
# ANTES (todo en checkout):
git checkout -- archivo           # Descartar cambios
git checkout otra-rama            # Cambiar rama
git checkout -b nueva-rama        # Crear rama

# AHORA (separado):
git restore archivo               # Descartar cambios (RECOMENDADO)
git switch otra-rama              # Cambiar rama (RECOMENDADO)
git switch -c nueva-rama          # Crear rama (RECOMENDADO)

# PERO checkout sigue funcionando (por compatibilidad)
```

**¿Cuál usar?**

- **git switch** → Solo para cambiar/crear ramas
- **git restore** → Solo para recuperar/descartar archivos
- **git checkout** → Ambos (vieja escuela, pero funciona)

🎯 Ejercicio práctico:

**Tu misión: Dominar la navegación Git**

```bash
# 1. Crear proyecto con historia
mkdir navegacion-git
cd navegacion-git
git init
echo "v1" > app.js && git add . && git commit -m "v1"
echo "v2" > app.js && git add . && git commit -m "v2"
echo "v3" > app.js && git add . && git commit -m "v3"

# 2. Practicar navegación
git checkout HEAD~1            # Ir a v2
cat app.js                     # Debería decir "v2"
git checkout HEAD~1            # Ir a v1
cat app.js                     # Debería decir "v1"

# 3. Crear ramas desde puntos históricos
git checkout -b experimento-v2 HEAD~2
git branch                     # Ver ramas

# 4. Recuperar archivos antiguos
echo "v4 modificado" > app.js
cat app.js                     # v4 modificado
git checkout HEAD -- app.js    # Recuperar v3 original
cat app.js                     # Debería decir "v3"

# 5. Descartar cambios
echo "cambio no deseado" >> app.js
git checkout -- app.js         # Descartar
cat app.js                     # Vuelve a v3
```

💭 Preguntas frecuentes:

**❓ ¿Qué pasa con mis cambios no commitados al cambiar de rama?**

```bash
# Depende:
# 1. Si los cambios NO conflictúan → Git los mantiene
# 2. Si los cambios CONFLICTÚAN → Git te avisa y no te deja cambiar
# 3. Siempre puedes usar git stash para guardarlos temporalmente
```

**❓ ¿Puedo cambiar a rama remota directamente?**

```bash
# Sí, pero primero necesitas una copia local
git checkout -b local-name origin/remote-branch
# o (Git 2.23+)
git switch -c local-name origin/remote-branch
```

**❓ ¿Checkout afecta el repositorio remoto?**

```bash
# NO, checkout solo afecta tu copia local
# Es 100% seguro para experimentar localmente
```

**❓ ¿Cómo saber a qué commit apunta HEAD?**

```bash
git log --oneline -1
# o
git rev-parse HEAD
# o
cat .git/HEAD
```

📊 Tabla de navegación:

| Quieres... | Comando viejo | Comando nuevo (2.23+) |
|-----------|--------------|----------------------|
| Cambiar rama | `git checkout rama` | `git switch rama` |
| Crear rama | `git checkout -b nueva` | `git switch -c nueva` |
| Descartar cambios | `git checkout -- archivo` | `git restore archivo` |
| Recuperar archivo viejo | `git checkout abc123 -- archivo` | `git restore -s abc123 -- archivo` |
| Ir a commit antiguo | `git checkout abc123` | `git switch --detach abc123` |

🎨 Visualizando checkout:

```
graph TD
    A[main: Commit C3] --> B[feature: Commit D2]
    A --> C[develop: Commit E1]
    
    D[Tu HEAD] -.->|git checkout feature| B
    D -.->|git checkout develop| C
    D -.->|git checkout main| A
    
    E[Working Directory] --> F{Contenido actual}
    F -->|checkout| G[Cambia según rama]
    
    style B fill:#e1f5fe
    style C fill:#f3e5f5
    style A fill:#e8f5e8
```

<div align="center">

**🎯 Punto Clave de git checkout:**

```diff
+ Es tu "teletransportador" entre ramas y commits
+ Te permite viajar en el tiempo del proyecto
- Puede ser confuso (tiene múltiples funciones)
+ Mejor usar `git switch` y `git restore` (moderno)
```

</div>

