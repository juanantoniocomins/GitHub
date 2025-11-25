# 📦 Mover carpeta dentro del repositorio usando Git (PowerShell)

A continuación tienes el procedimiento completo realizado para mover la carpeta **"01 - Conceptos Básicos de la Nube"** a su nuevo destino dentro del repositorio, incluyendo el origen, el destino y todos los comandos utilizados paso a paso.

---

## 📂 Origen y destino

- **Carpeta origen:**  
  `01 - Conceptos Básicos de la Nube`

- **Carpeta destino:**  
  `Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/01 - Conceptos Básicos de la Nube`

---

## 📝 Paso a paso (completo y listo para usar en GitHub)

```powershell
# 1. Ir al directorio donde se guardará el repositorio
cd C:\github

# 2. Clonar el repositorio
git clone https://github.com/juanantoniocomins/Cloud_computing.git

# 3. Entrar en el repositorio
cd Cloud_computing

# 4. Crear una rama nueva para mover la carpeta
git checkout -b mover-carpeta-conceptos-a-aws

# 5. Obtener la información más reciente del repositorio
git fetch origin
git pull origin main

# 6. Crear la carpeta destino (si no existe)
mkdir "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)"

# 7. Mover la carpeta al nuevo destino
git mv "01 - Conceptos Básicos de la Nube" "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/01 - Conceptos Básicos de la Nube"

# 8. Verificar los cambios
git status

# 9. Configurar identidad en Git (solo si lo solicita)
git config --global user.name "Juan Antonio Comins"
git config --global user.email "juanancomins@gmail.com"

# 10. Crear el commit
git commit -m "Mover carpeta de conceptos básicos a AWS Cloud Practitioner"

# 11. Subir la rama al repositorio remoto
git push -u origin mover-carpeta-conceptos-a-aws

🔀 Crear Pull Request

Después del push, Git mostrará un enlace similar a este:
https://github.com/juanantoniocomins/Cloud_computing/pull/new/mover-carpeta-conceptos-a-aws
Puedes abrirlo para crear el Pull Request y completar el proceso.

✅ Resultado final

✔ La carpeta se movió correctamente.
✔ Los cambios ya están en la rama mover-carpeta-conceptos-a-aws.
✔ Solo queda revisar y fusionar el Pull Request.

## 📁 Moviendo otra carpeta: "02 - Procesamiento en la Nube"

Este es el procedimiento completo realizado en PowerShell para mover la carpeta **"02 - Procesamiento en la Nube"** al destino dentro del repositorio.

### 🔧 Comandos ejecutados en PowerShell

```powershell
**PS C:\github\Cloud_computing>** git checkout -b mover-carpeta-procesamiento-a-aws
Switched to a new branch 'mover-carpeta-procesamiento-a-aws'

**PS C:\github\Cloud_computing>** git fetch origin
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 969 bytes | 161.00 KiB/s, done.
From https://github.com/juanantoniocomins/Cloud_computing
   94decb6..f33b9cf  main       -> origin/main

**PS C:\github\Cloud_computing>** git pull origin main
From https://github.com/juanantoniocomins/Cloud_computing
 * branch            main       -> FETCH_HEAD
Updating c6865df..f33b9cf
Fast-forward

**PS C:\github\Cloud_computing>** mkdir "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)"
New-Item: An item with the specified name C:\github\Cloud_computing\Amazon AWS\AWS Cloud Practitioner Essentials (25-26) already exists.

**PS C:\github\Cloud_computing>** git mv "02 - Procesamiento en la Nube" "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube"

**PS C:\github\Cloud_computing>** git status
On branch mover-carpeta-procesamiento-a-aws
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    02 - Procesamiento en la Nube/README.md -> Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube/README.md

**PS C:\github\Cloud_computing>** git commit -m "Mover carpeta de procesamiento en la nube a AWS Cloud Practitioner"
[mover-carpeta-procesamiento-a-aws 1afc921] Mover carpeta de procesamiento en la nube a AWS Cloud Practitioner
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename {02 - Procesamiento en la Nube => Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube}/README.md (100%)

**PS C:\github\Cloud_computing>** git push -u origin mover-carpeta-procesamiento-a-aws
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 4 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 586 bytes | 586.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote:
remote: Create a pull request for 'mover-carpeta-procesamiento-a-aws' on GitHub by visiting:
remote:      https://github.com/juanantoniocomins/Cloud_computing/pull/new/mover-carpeta-procesamiento-a-aws
remote:
To https://github.com/juanantoniocomins/Cloud_computing.git
 * [new branch]      mover-carpeta-procesamiento-a-aws -> mover-carpeta-procesamiento-a-aws
branch 'mover-carpeta-procesamiento-a-aws' set up to track 'origin/mover-carpeta-procesamiento-a-aws'.

🔀 Crear Pull Request

Abre el enlace que Git mostró después del push:

https://github.com/juanantoniocomins/Cloud_computing/pull/new/mover-carpeta-procesamiento-a-aws

y crea el Pull Request para fusionar los cambios en main.

✅ Resultado final

Carpeta "02 - Procesamiento en la Nube" movida correctamente.
Cambios disponibles en la rama mover-carpeta-procesamiento-a-aws.
Pull Request listo para revisión y fusión.

