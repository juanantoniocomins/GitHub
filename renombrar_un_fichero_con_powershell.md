# 📦 Renombrar archivo dentro del repositorio usando Git (PowerShell)

A continuación tienes el procedimiento completo para renombrar el archivo **"Introducción a Amazon EC2.md"** dentro del repositorio, manteniendo el historial del fichero y registrando correctamente el cambio como un movimiento.

---

## 📂 Archivo origen y nuevo nombre

- **Archivo original:**  
  `Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube/Introducción a Amazon EC2.md`

- **Nuevo nombre:**  
  `Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube/01-Fundamentos_de_Amazon_EC2.md`

---

## 📝 Paso a paso (completo y listo para usar en GitHub)

```powershell
# 1. Ir al directorio donde se encuentra el repositorio
cd C:\github\Cloud_computing

# 2. Crear una nueva rama para el cambio
git checkout -b renombrar-fichero-ec2

# 3. Renombrar el archivo usando git mv
git mv "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube/Introducción a Amazon EC2.md" `
       "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/02 - Procesamiento en la Nube/01-Fundamentos_de_Amazon_EC2.md"

# 4. Verificar que Git detecta el cambio
git status

# 5. Confirmar (commit) los cambios
git commit -m "Renombrado archivo: Introducción a Amazon EC2 → Fundamentos de Amazon EC2"

# 6. Subir la rama al repositorio remoto
git push origin renombrar-fichero-ec2

