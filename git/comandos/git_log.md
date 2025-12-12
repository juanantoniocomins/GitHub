# 🎯 Comando #5: git log - La Máquina del Tiempo

⏳ El problema del "olvido":

```text
Has trabajado semanas en un proyecto...
❌ ¿Qué cambios hice ayer?
❌ ¿Quién modificó este archivo?
❌ ¿Cuándo introdujimos ese bug?
❌ ¿Cómo estaba el código hace un mes?
```

🕰️ La solución del "historial completo":

```bash
# Ver TODA la historia del proyecto
git log
```

**Salida típica:**

```text
commit a1b2c3d4e5f6789012345678901234567890abcd
Author: Juan Pérez <juan@email.com>
Date:   Mon Mar 18 10:30:45 2024 -0500

    feat: agregar sistema de comentarios
    
    - Crear modelo Comment
    - Agregar formulario de comentarios
    - Implementar validaciones
    
    Closes #45

commit b2c3d4e5f6789012345678901234567890abcde1
Author: María Gómez <maria@email.com>
Date:   Fri Mar 15 14:20:30 2024 -0500

    fix: corregir bug en cálculo de precios
    
    El cálculo no incluía el IVA correctamente
    para productos internacionales.
```

🎨 Formatos de visualización:

```bash
# 1. Una línea por commit (compacto)
git log --oneline
# a1b2c3d feat: agregar sistema de comentarios
# b2c3d4e fix: corregir bug en cálculo de precios

# 2. Con gráfico de ramas
git log --graph --oneline --all
# * a1b2c3d (HEAD -> main) feat: agregar comentarios
# * b2c3d4e fix: bug precios
# | * c3d4e5f (feature/login) feat: login con Google
# |/
# * d4e5f678 chore: actualizar dependencias

# 3. Con estadísticas
git log --stat
# commit a1b2c3d...
#  app/models/comment.rb | 45 +++++++++++++++++++++
#  app/views/comments/   | 30 ++++++++++++++
#  2 files changed, 75 insertions(+)

# 4. Con cambios específicos
git log -p  # patch, muestra los diffs
```

🔍 Búsquedas específicas:

```bash
# 1. Por autor
git log --author="Juan"
git log --author="juan@email.com"

# 2. Por fecha
git log --since="2024-01-01"
git log --until="2024-03-15"
git log --since="2 weeks ago"
git log --after="yesterday"

# 3. Por mensaje
git log --grep="bug"
git log --grep="feat" -i  # -i para case insensitive

# 4. Por archivo
git log -- app/models/user.rb
git log --follow -- app/models/user.rb  # Sigue renombres

# 5. Por cantidad
git log -5  # Últimos 5 commits
git log -n 10 --oneline

# 6. Combinaciones
git log --author="Juan" --since="1 month ago" --oneline
```

📊 Visualizaciones avanzadas:

```bash
# 1. Formato personalizado
git log --pretty=format:"%h - %an, %ar : %s"
# a1b2c3d - Juan Pérez, 2 days ago : feat: agregar comentarios

# 2. Con colores
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'

# 3. Árbol de archivos
git log --name-status
# M    app/models/comment.rb
# A    app/views/comments/index.html.erb

# 4. Resumen por día
git log --since="30 days ago" --pretty=format:"%ad" --date=short | uniq -c
#   5 2024-03-18
#   3 2024-03-17
#   2 2024-03-15
```

💡 Códigos de formato:

| Código | Significado | Ejemplo |
|--------|------------|---------|
| %h | Hash abreviado | a1b2c3d |
| %H | Hash completo | a1b2c3d... |
| %an | Nombre autor | Juan Pérez |
| %ae | Email autor | juan@email.com |
| %ad | Fecha autor | Mon Mar 18 10:30:45 2024 |
| %ar | Fecha relativa | 2 days ago |
| %s | Asunto | feat: agregar comentarios |
| %b | Cuerpo | - Crear modelo Comment... |
| %d | Referencias | (HEAD -> main, origin/main) |

🧪 Ejemplos prácticos:

**Caso 1: Investigar un bug**

```bash
# Encontraste un bug en user_controller.rb
# ¿Cuándo se introdujo?

git log -p -- app/controllers/user_controller.rb
# Revisas los cambios históricos
# Encuentras el commit problemático: b2c3d4e

git show b2c3d4e
# Ves exactamente qué cambió
# ¡Encontraste el culpable!
```

**Caso 2: Ver tu trabajo de la semana**

```bash
# Lunes por la mañana: ¿Qué hice la semana pasada?
git log --author="yo@email.com" --since="last monday" --until="friday" --oneline
# b2c3d4e fix: bug en login
# c3d4e5f feat: dark mode
# d4e5f678 refactor: clean up CSS
# ✅ Ahora sé por dónde continuar
```

**Caso 3: Preparar changelog**

```bash
# Para el release 2.0, necesitas un changelog
git log --since="v1.9.0" --pretty=format:"- %s (%h, %ad)" --date=short
# - feat: agregar export a PDF (a1b2c3d, 2024-03-18)
# - fix: corregir timeout en API (b2c3d4e, 2024-03-17)
# - docs: actualizar README (c3d4e5f, 2024-03-15)
```

🌍 Flujo de trabajo real:

**Desarrollador senior revisando código:**

```bash
# 1. Ver actividad reciente del equipo
git log --since="1 week ago" --pretty=format:"%an: %s" | sort | uniq
# Ana García: fix: bug en checkout
# Carlos López: feat: filtros de búsqueda
# Juan Pérez: refactor: auth middleware
# María Gómez: docs: actualizar API docs

# 2. Revisar cambios en archivo crítico
git log --oneline -10 -- app/utils/security.js
# Identifica cambios recientes en seguridad

# 3. Ver contribuciones por persona
git shortlog -sn --since="1 month ago"
#    15 Juan Pérez
#    10 Ana García
#     8 Carlos López
#     5 María Gómez

# 4. Encontrar commit que introdujo feature específica
git log --all --grep="login" --oneline
```

🚨 Errores comunes:

**❌ Problema: Demasiada información**

```bash
# git log muestra miles de líneas
# Solución: filtrar y limitar

git log --oneline -20  # Solo últimos 20, compacto
git log --since="1 month ago"  # Solo este mes
git log --grep="feat"  # Solo commits de features
```

**❌ Problema: No veo ramas remotas**

```bash
# git log solo muestra local
# Solución: incluir remoto

git log --all --graph --oneline
git fetch  # Traer info remota primero
git log origin/main..HEAD  # Ver commits locales no enviados
```

**❌ Problema: Hash difíciles de leer**

```bash
# Configurar alias con colores
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Ahora usa: git lg
```

🔧 Configuraciones útiles:

```bash
# 1. Alias para log bonito
git config --global alias.lg "log --oneline --graph --all"

# 2. Mostrar ramas siempre
git config --global log.decorate auto

# 3. Paginación personalizada
git config --global core.pager "less -RFX"

# 4. Formato por defecto
git config --global pretty.format "%C(yellow)%h %C(green)%ad %C(blue)%an %C(red)%d %C(reset)%s"

# 5. Ver upstream status
git config --global log.showSignature true
```

🎯 Ejercicio práctico:

**Tu misión: Convertirte en detective de Git**

```bash
# 1. Crear repositorio con historia
mkdir detective-git
cd detective-git
git init

# 2. Crear historia de commits
echo "# Proyecto" > README.md
git add . && git commit -m "docs: README inicial"

echo "console.log('v1')" > app.js
git add . && git commit -m "feat: app inicial" --author="Ana <ana@email.com>"

echo "// bug aquí" >> app.js
git add . && git commit -m "fix: bug crítico" --author="Buggy <bug@email.com>"

echo "// mejora" >> app.js
git add . && git commit -m "refactor: mejorar código" --author="Carlos <carlos@email.com>"

# 3. Investigar
# ¿Quién introdujo el bug?
git log --grep="bug" --oneline

# ¿Qué archivos cambió Carlos?
git log --author="Carlos" --name-status

# ¿Cuántos commits por autor?
git shortlog -sn

# ¿Timeline completo?
git log --pretty=format:"%ad %an: %s" --date=short
```

💭 Preguntas frecuentes:

**❓ ¿Cómo veo commits entre dos tags?**

```bash
git log v1.0.0..v2.0.0 --oneline
# Muestra commits después de v1.0.0 hasta v2.0.0
```

**❓ ¿Cómo encuentro commits que borraron código específico?**

```bash
git log -p -S "funciónEliminada" --all
# Busca en todo el historial
```

**❓ ¿Cómo veo solo mis commits no pusheados?**

```bash
git log @{u}.. --oneline
# o
git log origin/main..HEAD --oneline
```

**❓ ¿Git log afecta el repositorio?**

```bash
# NO, git log es solo de lectura
# Solo muestra información, no cambia nada
# Es completamente seguro usarlo
```

📊 Resumen de opciones:

| Necesitas... | Comando |
|-------------|---------|
| Vista rápida | `git log --oneline` |
| Ver ramas | `git log --graph --all` |
| Buscar texto | `git log --grep="texto"` |
| Filtrar por autor | `git log --author="nombre"` |
| Filtrar por fecha | `git log --since="fecha"` |
| Ver cambios | `git log -p` |
| Ver estadísticas | `git log --stat` |
| Formato personal | `git log --pretty=format:"..."` |

🎨 Visualizando el historial:

```
timeline
    title Historia del Proyecto
    section Marzo 2024
        Día 18 : feat: comentarios<br>(Juan)
        Día 17 : fix: bug precios<br>(María)
        Día 15 : chore: dependencias<br>(Carlos)
    section Febrero 2024
        Día 28 : feat: login social<br>(Ana)
        Día 25 : docs: API<br>(Juan)
```

<div align="center">

**🎯 Punto Clave de git log:**

```diff
+ Es tu "máquina del tiempo" Git
+ Te permite investigar, auditar, entender
+ Sin esto, no sabes de dónde vienes
+ Esencial para debugging y onboarding
```

</div>

