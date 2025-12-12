# 🎯 Comando #10: git push - Compartir tu Trabajo

📤 El problema del "trabajo aislado":

```text
Has trabajado duro por días...
❌ Tu equipo no puede ver tus cambios
❌ No hay backup de tu trabajo
❌ No puedes colaborar en reviews
❌ Tu código solo existe en tu computadora
```

🌍 La solución del "compartir con el mundo":

```bash
# Enviar tus commits al repositorio remoto
git push origin main

# Si todo sale bien:
# Enumerating objects: 5, done.
# Counting objects: 100% (5/5), done.
# Writing objects: 100% (3/3), 300 bytes | 300.00 KiB/s, done.
# Total 3 (delta 0), reused 0 (delta 0)
# To github.com:usuario/repo.git
#   abc123..def456  main -> main
```

🧠 ¿Qué hace realmente git push?

**git push envía:**

- Tus commits nuevos (que el remoto no tiene)
- Tus branches nuevos (que el remoto no conoce)
- Actualiza referencias (dónde apuntan las ramas)

**Visualmente:**

```text
TÚ (local):           A---B---C  (main)
REMOTO (origin):      A---B

git push origin main ↓

REMOTO después:       A---B---C  (main)
                     (tus commits C ahora están en GitHub/GitLab)
```

🧪 Modos de push:

**1. Push simple**

```bash
git push origin main
# Envía rama main al remoto origin
```

**2. Push con upstream tracking**

```bash
# Primera vez (establece relación):
git push -u origin feature/nueva
# -u = --set-upstream

# Después (ya sabe a dónde):
git push
```

**3. Push forzado (¡CUIDADO!)**

```bash
git push --force origin main
# o (más seguro)
git push --force-with-lease
```

**4. Push de todas las ramas**

```bash
git push --all origin
# Envía TODAS tus ramas locales
```

**5. Push de tags**

```bash
git push --tags
# Envía tags al remoto
```

💡 Configuración recomendada:

```bash
# 1. Configurar push por defecto
git config --global push.default current
# Solo empuja la rama actual

# 2. Configurar para usar --force-with-lease por defecto
git config --global push.useForceIfIncludes true

# 3. Configurar upstream automático
git config --global push.autoSetupRemote true

# 4. Ver configuración actual
git config --get push.default
```

🚨 Errores comunes y soluciones:

**❌ Error: "failed to push some refs"**

```bash
git push
# ! [rejected]        main -> main (non-fast-forward)
# error: failed to push some refs

# CAUSA: El remoto tiene commits que tú no tienes
# SOLUCIÓN:
git pull  # Traer cambios remotos primero
git push  # Intentar de nuevo
```

**❌ Error: "src refspec does not match any"**

```bash
git push origin rama-inexistente
# error: src refspec rama-inexistente does not match any

# CAUSA: La rama local no existe
# SOLUCIÓN: Crear la rama primero
git checkout -b rama-inexistente
git push -u origin rama-inexistente
```

**❌ Error: "permission denied"**

```bash
git push
# fatal: Authentication failed for 'https://github.com/...'

# SOLUCIONES:
# 1. Verificar credenciales
git config --get credential.helper

# 2. Usar SSH en lugar de HTTPS
git remote set-url origin git@github.com:usuario/repo.git

# 3. Renovar token/contraseña
git credential reject
git push  # Te pedirá credenciales nuevas
```

🌍 Caso real: Flujo de trabajo profesional

**Desarrollador en startup tech:**

```bash
# LUNES: Empieza nueva feature
git checkout main
git pull  # Sincronizar
git checkout -b feature/chat-realtime

# Trabaja durante el día...
git add .
git commit -m "feat: add socket.io setup"
git push -u origin feature/chat-realtime
# ✅ Crea Pull Request en GitHub

# MARTES: Continúa feature
git add .
git commit -m "feat: implement message broadcasting"
git push  # Ya tiene upstream, solo `git push`

# MIÉRCOLES: Recibe feedback en PR
# Hacer cambios solicitados
git add .
git commit -m "fix: address PR comments"
git push

# JUEVES: PR aprobado, merge a main
# En GitHub: Merge pull request
# Localmente:
git checkout main
git pull  # Traer el merge
git branch -d feature/chat-realtime  # Limpiar rama local
git push origin --delete feature/chat-realtime  # Limpiar remota
```

🔍 Push seguro: force vs force-with-lease

**⚠️ git push --force (PELIGROSO)**

```bash
# Sobreescribe el remoto SIN verificar
# Puedes borrar trabajo de otros
# SOLO usar en ramas privadas/experimentales
```

**✅ git push --force-with-lease (RECOMENDADO)**

```bash
# Verifica que el remoto no cambió desde tu último fetch
# Si alguien más hizo push, te avisa
# Mucho más seguro

# Configurar como default:
git config --global alias.pushf "push --force-with-lease"
# Usar: git pushf
```

🎮 Push en diferentes situaciones:

**Situación 1: Primera vez en rama nueva**

```bash
git checkout -b feature/nueva
# ...commits...
git push -u origin feature/nueva
# -u establece tracking para futuros push/pull
```

**Situación 2: Rama existente con tracking**

```bash
git push
# Como ya tiene upstream, no necesita especificar
```

**Situación 3: Después de rebase local**

```bash
# Rebaseaste localmente, historia cambió
git push --force-with-lease
# Avisa si alguien más hizo push mientras
```

**Situación 4: Subir tags**

```bash
git tag v1.2.3
git push --tags
# o un tag específico
git push origin v1.2.3
```

🔧 Buenas prácticas de push:

**1. Push frecuentemente:**

```bash
# Mejor: Varios push pequeños al día
# Que: Un push enorme al final de la semana

# Razones:
# • Backup automático
# • Feedback temprano
# • Menos conflicto en merge
```

**2. Siempre pull antes de push:**

```bash
# Flujo seguro:
git pull --rebase  # Actualizar con remoto
git push           # Subir tus cambios
```

**3. Usar branches para features:**

```bash
# NO:
git commit -m "mil cambios"
git push origin main

# SÍ:
git checkout -b feature/especifica
git commit -m "cambio específico"
git push -u origin feature/especifica
# Crear PR para revisión
```

**4. Mensajes de commit claros:**

```bash
git commit -m "fix: resolve login timeout issue"
git push
# vs
git commit -m "cambios"
git push  # 😓 Nadie entiende qué cambió
```

🎯 Ejercicio práctico:

**Tu misión: Dominar todos los escenarios de push**

```bash
# 1. Crear repositorio local y remoto (simulado)
mkdir proyecto-push
cd proyecto-push
git init
echo "# Proyecto" > README.md
git add . && git commit -m "Initial commit"

# 2. Crear repositorio "remoto" (otra carpeta)
cd ..
mkdir remoto-simulado
cd remoto-simulado
git init --bare
cd ../proyecto-push

# 3. Configurar remoto
git remote add origin ../remoto-simulado

# 4. Primer push (rama main)
git push -u origin main

# 5. Crear feature branch y push
git checkout -b feature/test
echo "nueva funcionalidad" >> README.md
git add . && git commit -m "feat: add test feature"
git push -u origin feature/test

# 6. Hacer más cambios y push simple
echo "más cambios" >> README.md
git add . && git commit -m "feat: improve feature"
git push  # Ya no necesita -u

# 7. Forzar push (simular rebase)
git rebase -i HEAD~2  # Combinar últimos 2 commits
git push --force-with-lease
```

💭 Preguntas frecuentes:

**❓ ¿Con qué frecuencia hacer push?**

```bash
# Mínimo: Al terminar una tarea lógica
# Ideal: 2-3 veces al día
# Máximo: Cada commit (si son pequeños y limpios)
# Regla: Push cuando otros podrían beneficiarse de ver tu código
```

**❓ ¿Push directo a main o por PR?**

```bash
# Proyectos pequeños/personales:
# git push origin main  # Directo está bien

# Proyectos de equipo/empresa:
# git push origin feature/nueva
# # Crear Pull Request para revisión
# # Solo maintainers mergean a main

# Open source:
# NUNCA push directo a main
# Siempre fork -> feature -> PR
```

**❓ ¿Qué pasa si hago push de algo sensible?**

```bash
# 1. Contraseñas/API keys:
# • git filter-repo (herramienta especial)
# • Contactar al admin del repo
# • Rotar las credenciales comprometidas

# 2. Archivos grandes:
# • git filter-repo --path archivo-grande --invert-paths
# • git push --force (cuidado!)

# Prevención: Usar .gitignore y git-secrets
```

**❓ ¿Cómo ver qué voy a push?**

```bash
# Ver commits locales no pusheados
git log origin/main..HEAD --oneline

# Ver diferencias con remoto
git diff origin/main..HEAD

# Push dry-run (simula)
git push --dry-run origin main
```

📊 Tabla de comportamientos:

| Comando | Comportamiento | Recomendado para |
|---------|---------------|------------------|
| `git push` | Push rama actual si tiene upstream | Día a día |
| `git push origin rama` | Push rama específica | Primera vez |
| `git push -u origin rama` | Push + establece upstream | Crear nueva rama |
| `git push --force-with-lease` | Push forzado seguro | Después de rebase |
| `git push --all` | Push todas las ramas | Migración/backup |
| `git push --tags` | Push todos los tags | Lanzar versión |

🎨 Visualizando push:

```
sequenceDiagram
    participant Local
    participant Remote
    participant GitHub

    Note over Local,Remote: Estado inicial
    Local->>Local: Trabajo local: commits C, D
    Local->>Remote: git push origin main
    
    Remote->>GitHub: Sube commits C y D
    GitHub-->>Remote: Confirmación
    
    Remote-->>Local: main -> main (abc123..def456)
    
    Note over GitHub: Ahora todos pueden ver<br/>tus commits C y D
```

<div align="center">

**🎯 Punto Clave de git push:**

```diff
+ Comparte tu trabajo con el mundo
+ Crea backup en la nube
+ Permite colaboración y revisión
+ Es el "publicar" de Git
```

</div>

