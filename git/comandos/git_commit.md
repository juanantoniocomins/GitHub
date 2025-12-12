# 🎯 Comando #3: git commit - Guardando Momentos

💾 El problema del "trabajo perdido":

```text
Has estado trabajando por horas...
❌ La computadora se apaga
❌ Borras archivos por error  
❌ No recuerdas qué cambiabas
❌ No puedes volver a versiones anteriores
```

✨ La solución de la "máquina del tiempo":

```bash
# Guardar todo lo preparado con git add
git commit -m "Mensaje descriptivo"

# Resultado:
[main 1a2b3c4] Mensaje descriptivo
 3 files changed, 50 insertions(+), 2 deletions(-)
```

🧠 ¿Qué es realmente un commit?

Un commit es:

```text
📦 Un "paquete" de cambios
📅 Un momento en el tiempo  
🔒 Un punto seguro al que volver
📝 Una anotación en tu historial
```

Piensa en commits como:

- 📸 Fotos de tu proyecto
- 🎮 Puntos de guardado en un videojuego
- 📚 Páginas en el libro de tu proyecto
- 🗺️ Marcadores en un mapa del desarrollo

🧪 Ejemplos de buenos commits:

```bash
# ❌ MAL - Mensajes vagos
git commit -m "cambios"
git commit -m "fix"
git commit -m "update"

# ✅ BIEN - Mensajes descriptivos
git commit -m "Agregar formulario de contacto"
git commit -m "Corregir bug en cálculo de precios"
git commit -m "Actualizar dependencias a versión 2.0"

# ✅ EXCELENTE - Mensajes detallados
git commit -m "feat: añadir autenticación con Google

- Implementar OAuth 2.0 flow
- Agregar botón de login con Google
- Crear página de callback
- Actualizar documentación

Closes #123"
```

📝 Convenciones de mensajes (estilo convencional):

```text
tipo(alcance): descripción breve

cuerpo (opcional)

pie de página (opcional)
```

**Tipos comunes:**

- **feat**: Nueva funcionalidad
- **fix**: Corrección de bug
- **docs**: Cambios en documentación
- **style**: Formato, punto y coma faltante
- **refactor**: Refactorización de código
- **test**: Agregar o corregir tests
- **chore**: Cambios en build, herramientas

**Ejemplo profesional:**

```bash
git commit -m "feat(auth): implementar login con Google

- Integrar SDK de Google OAuth
- Crear componente GoogleLoginButton
- Manejar tokens JWT en frontend

Closes #45, #78"
```

💡 Modificando commits:

```bash
# 1. Commit con mensaje incorrecto
git commit -m "cambios"

# 2. Corregir el ÚLTIMO commit
git commit --amend -m "feat: agregar navbar responsive"

# 3. Si también olvidaste archivos
git add archivo-olvidado.js
git commit --amend --no-edit  # Mantiene el mismo mensaje

# 4. Verificar que se actualizó
git log --oneline -1  # Muestra el último commit
```

🔍 Ver commits anteriores:

```bash
# 1. Ver historial completo
git log

# 2. Ver resumen de una línea
git log --oneline

# 3. Ver cambios específicos de un commit
git show abc123  # Donde abc123 es el hash del commit

# 4. Ver historial con gráfico
git log --graph --oneline --all

# 5. Ver commits de un archivo específico
git log --follow archivo.js

# 6. Ver commits de un autor
git log --author="nombre"

# 7. Ver commits entre fechas
git log --since="2024-01-01" --until="2024-12-31"
```

🎮 Estados del working directory:

**Antes del commit:**

```bash
# Tienes cambios no comprometidos
git status
# Changes to be committed:
#   (archivos en staging - VERDE)
# Changes not staged for commit:
#   (archivos modificados - ROJO)
# Untracked files:
#   (archivos nuevos - ROJO)
```

**Después del commit:**

```bash
# Todo limpio (si commiteaste todo)
git status
# On branch main
# nothing to commit, working tree clean

# ¡Felicidades! Tu trabajo está seguro 🎉
```

🌍 Caso real: Feature development:

```bash
# Día 1: Empiezo una nueva feature
git checkout -b feature/login

# Trabajo en varios archivos...
vim auth.js
vim styles.css
vim login.html

# Hago commits lógicos y pequeños
git add auth.js
git commit -m "feat: crear módulo de autenticación"

git add styles.css login.html
git commit -m "style: diseñar formulario de login"

# Día 2: Encuentro un bug en auth.js
# Modifico el archivo
vim auth.js

# Hago un commit de fix
git add auth.js
git commit -m "fix: validar email en auth module"

# Al final tengo 3 commits limpios y entendibles
git log --oneline
# abc123 fix: validar email en auth module
# def456 style: diseñar formulario de login
# ghi789 feat: crear módulo de autenticación
```

🚨 Errores comunes:

**❌ Error 1: Commit sin mensaje (abre editor)**

```bash
# Si olvidas -m, se abre el editor (vim/nano)
# Para salir sin commit:
# 1. En vim: :q!
# 2. En nano: Ctrl+X, luego N

# Para configurar mensaje por defecto:
git config --global core.editor "code --wait"  # Usar VS Code
```

**❌ Error 2: Commits demasiado grandes**

```bash
# Síntoma: Un commit con 20 archivos cambiados
# Problema: Difícil de revertir, difícil de entender

# Solución: Commits pequeños y frecuentes
# Regla: 1 commit = 1 cosa lógica completada
```

**❌ Error 3: Commits con código roto**

```bash
# Síntoma: Commit que rompe el build
# Solución: Siempre probar antes de commitear

# Herramientas útiles:
npm test       # Correr tests
npm run build  # Verificar que compila
git diff       # Revisar cambios
```

📊 Tabla: Tipos de commits y cuándo hacerlos

| Tipo | Frecuencia | Tamaño | Ejemplo |
|------|-----------|--------|---------|
| Feature | Cuando completas una funcionalidad | Medio | "feat: añadir carrito de compras" |
| Fix | Cuando arreglas un bug | Pequeño | "fix: corregir cálculo de IVA" |
| Refactor | Cuando mejoras código sin cambiar funcionalidad | Variable | "refactor: optimizar función de búsqueda" |
| Chore | Cuando actualizas herramientas/config | Pequeño | "chore: actualizar webpack a v5" |
| Docs | Cuando cambias documentación | Pequeño | "docs: agregar ejemplos de uso" |
| Style | Cuando cambias formato | Pequeño | "style: corregir indentación" |

🎯 Ejercicio práctico:

**Tu misión: Crear una serie de commits limpios**

```bash
# 1. Crear proyecto simple
mkdir ejercicio-commits
cd ejercicio-commits
git init

# 2. Crear estructura básica
echo "# Mi Proyecto" > README.md
git add README.md
git commit -m "docs: crear README inicial"

# 3. Añadir archivo HTML
echo "<html><body><h1>Hola</h1></body></html>" > index.html
git add index.html
git commit -m "feat: crear página principal"

# 4. Mejorar el HTML
echo "<p>Bienvenido al proyecto</p>" >> index.html
git add index.html
git commit -m "feat: agregar mensaje de bienvenida"

# 5. Ver tu historial
git log --oneline --graph

# Deberías ver algo como:
# * 789abc feat: agregar mensaje de bienvenida
# * 456def feat: crear página principal  
# * 123abc docs: crear README inicial
```

🔧 Configuraciones avanzadas:

```bash
# 1. Configurar editor preferido
git config --global core.editor "code --wait"

# 2. Plantilla para mensajes de commit
echo "## Tipo: feat|fix|docs|style|refactor|test|chore
## Alcance: (opcional) qué parte del proyecto
## Descripción: qué cambiaste y por qué
## 
## Cuerpo: (opcional) detalles adicionales
## 
## Footer: (opcional) issues cerrados, breaking changes" > ~/.gitmessage
git config --global commit.template ~/.gitmessage

# 3. Ver commits bonitos
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Ahora usa: git lg
```

💭 Preguntas frecuentes:

**❓ ¿Cuántos commits debería hacer?**

```text
✅ BUENO: Varios commits pequeños al día
❌ MAL: Un commit gigante al final de la semana

Regla general: Haz commit cuando:
• Termines una lógica lógica
• Arregles un bug específico  
• Termines de trabajar por hoy
• Alguien más necesita tus cambios
```

**❓ ¿Puedo cambiar commits viejos?**

```bash
# Sí, con cuidado (solo en tu rama local)
# Para cambiar el penúltimo commit:
git rebase -i HEAD~2
# En el editor, cambia "pick" por "edit"
# Luego: git commit --amend
# Finalmente: git rebase --continue

# ⚠️ ADVERTENCIA: No hagas esto en commits ya subidos a remoto
# Podrías causar problemas a otros desarrolladores
```

**❓ ¿Qué es un "commit vacío"?**

```bash
# Un commit sin cambios (solo mensaje)
git commit --allow-empty -m "chore: inicio de sprint"

# Útil para:
# • Marcar hitos del proyecto
# • Separar trabajo entre sprints
# • Iniciar nuevas features
```

🎨 Visualizando el historial:

```text
main
  │
  ├─○ feat: agregar navbar (abc123)
  │
  ├─○ fix: corregir enlace roto (def456)
  │
  ├─○ docs: actualizar README (ghi789)
  │
  └─○ chore: actualizar dependencias (jkl012)
```

Cada ○ es un commit seguro al que puedes volver:

```bash
# Volver al commit abc123
git checkout abc123

# Crear rama desde ese commit
git checkout -b experimento abc123

# Ver cómo estaba el proyecto en esa fecha
git show abc123:archivo.js
```

<div align="center">

**🎯 Punto Clave de git commit:**

```diff
+ Es la "foto" de tu proyecto en un momento
+ Cada commit debería hacer UNA cosa bien
+ Mensajes claros = historial comprensible  
+ Commits pequeños = reversiones fáciles
```

</div>

