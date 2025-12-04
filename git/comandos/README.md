# 📚 Resumen de Comandos Git

## Tabla de Comandos Esenciales

| Comando | ¿Para qué sirve? | Nivel |
|---------|-----------------|-------|
| `git init` | Inicializa repositorio local | 🟢 Básico |
| `git clone` | Copia repositorio remoto | 🟢 Básico |
| `git status` | Muestra estado del repositorio | 🟢 Básico |
| `git add` | Añade cambios al staging | 🟢 Básico |
| `git commit` | Guarda versión de cambios | 🟢 Básico |
| `git diff` | Muestra diferencias entre versiones | 🟡 Intermedio |
| `git log` | Muestra historial de commits | 🟡 Intermedio |
| `git branch` | Gestiona ramas | 🟡 Intermedio |
| `git checkout` | Cambia entre ramas o commits | 🟡 Intermedio |
| `git merge` | Fusiona ramas | 🔴 Avanzado |
| `git pull` | Actualiza local desde remoto | 🔴 Avanzado |
| `git push` | Sube commits al remoto | 🔴 Avanzado |
| `git remote` | Gestiona conexiones remotas | 🔴 Avanzado |

---

## 🟢 Comandos Básicos (Esenciales para empezar)

Estos comandos son fundamentales y deberías dominarlos primero:

- **git init**: Crea un nuevo repositorio Git desde cero
- **git clone**: Obtiene una copia de un repositorio existente
- **git status**: Te dice qué archivos han cambiado
- **git add**: Prepara archivos para el próximo commit
- **git commit**: Guarda permanentemente tus cambios

## 🟡 Comandos Intermedios (Para trabajar eficientemente)

Una vez domines los básicos, estos te harán más productivo:

- **git diff**: Examina exactamente qué líneas cambiaron
- **git log**: Explora la historia del proyecto
- **git branch**: Crea y gestiona diferentes líneas de desarrollo
- **git checkout**: Navega entre ramas y versiones

## 🔴 Comandos Avanzados (Para colaboración)

Esenciales para trabajar en equipo y con repositorios remotos:

- **git merge**: Une diferentes líneas de desarrollo
- **git pull**: Sincroniza tu código con el servidor
- **git push**: Comparte tus cambios con el equipo
- **git remote**: Configura conexiones con servidores

---

## 🎯 Flujo de Trabajo Típico

```bash
# 1. Obtener o crear repositorio
git clone https://github.com/usuario/proyecto.git  # O git init

# 2. Ver estado actual
git status

# 3. Hacer cambios en archivos...
# (editar código)

# 4. Ver qué cambió
git diff

# 5. Preparar cambios
git add archivo.js

# 6. Confirmar cambios
git commit -m "feat: nueva funcionalidad"

# 7. Sincronizar con remoto
git pull origin main

# 8. Subir cambios
git push origin main
```

---

## 💡 Consejos para Aprender

1. **Empieza por los básicos** 🟢: Domina init, add, commit, status
2. **Practica diariamente** 📅: Usa Git en todos tus proyectos
3. **Lee los mensajes de error** 🔍: Git te explica qué salió mal
4. **Usa las guías** 📚: Cada README tiene ejemplos prácticos
5. **No tengas miedo** 💪: Git casi siempre te permite deshacer

---

## 🚀 Recursos Adicionales

- **Documentación oficial**: [git-scm.com](https://git-scm.com)
- **Práctica interactiva**: [learngitbranching.js.org](https://learngitbranching.js.org)
- **Cheat sheet**: [github.com/github/training-kit](https://github.com/github/training-kit)

---

<div align="center">

**¿Listo para dominar Git?** 🎉

Empieza con los comandos básicos y avanza progresivamente.  
Cada guía incluye ejemplos prácticos y ejercicios.

**¡Feliz coding!** 💻✨

</div>
