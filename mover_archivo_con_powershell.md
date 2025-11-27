# 📦 Mover archivo dentro del repositorio usando Git (PowerShell)

A continuación tienes el procedimiento completo realizado para mover el archivo **"04-Quien_cuida_de_AWS.md"** a su nuevo destino dentro del repositorio, incluyendo el origen, el destino y todos los comandos utilizados paso a paso.

---

## 📂 Origen y destino

- **Archivo origen:**  
  `Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/04-Quien_cuida_de_AWS.md`

- **Carpeta destino:**  
  `Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/01 - Conceptos Básicos de la Nube/`

---

## 📝 Paso a paso (completo y listo para usar en GitHub)

```powershell
# 1. Ir al directorio donde se guardará el repositorio
cd C:\Users\Usuario

# 2. Clonar el repositorio
git clone https://github.com/juanantoniocomins/Cloud_computing.git

# 3. Entrar en el repositorio
cd Cloud_computing

# 4. Mover el archivo al nuevo destino usando PowerShell
Move-Item -Path "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/04-Quien_cuida_de_AWS.md" `
          -Destination "Amazon AWS/AWS Cloud Practitioner Essentials (25-26)/01 - Conceptos Básicos de la Nube/"

# 5. Verificar los cambios detectados por Git
git status

# 6. Añadir todos los cambios (archivo movido)
git add -A

# 7. Crear el commit con los cambios realizados
git commit -m "Mover 04-Quien_cuida_de_AWS.md al directorio 01 - Conceptos Básicos de la Nube"

# 8. Subir los cambios al repositorio remoto
git push origin main


✅ Resultado final

✔ El archivo se movió correctamente al directorio final.
✔ Los cambios fueron confirmados en un commit.
✔ El repositorio remoto ya refleja la nueva ubicación del archivo.
