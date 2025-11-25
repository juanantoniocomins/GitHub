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

