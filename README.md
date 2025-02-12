# 🚀 Guía Completa para Usar GitHub 💻  

¡Guía de GitHub! 
---

## 📌 ¿Qué es GitHub?  
GitHub es una plataforma que permite almacenar código, colaborar en proyectos y hacer control de versiones utilizando **Git**.  

Es **esencial** para cualquier desarrollador y es ampliamente usado en proyectos de código abierto, empresas y desarrollo personal.  

---

## 🎯 Instalación de Git  
Antes de usar GitHub, necesitas instalar **Git** en tu computadora.  

### 🔹 En macOS:  
```sh
brew install git
```
### 🔹 En windows:
#### Descarga Git desde <https://git-scm.com/>
 e instálalo.

### 🔹 En Linux (Ubuntu/Debian):
```sh
sudo apt update
sudo apt install git
```

#### Verifica que Git se instaló correctamente ✅:
```sh
git --version
```

---

## 🔑 Configurar Git por primera vez  
Antes de usar Git, configúralo con tu nombre y correo:  

```sh
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
```

#### Verifica la configuración 👀

```sh
git config --list
```

---

## 🛠️ Comandos esenciales de Git  

Aquí tienes una lista detallada de comandos esenciales que te ayudarán a gestionar un repositorio en Git y colaborar en proyectos de GitHub.

### 🔹 1. Ver el estado de tu repositorio  
Para ver qué archivos han cambiado, cuáles están listos para ser confirmados y si hay archivos sin seguimiento:  

```sh
git status
```

### 🔹 2. Agregar archivos al área de staging
Si quieres añadir un archivo específico al área de staging antes de hacer un commit:

```sh
git add nombre-del-archivo
```

si quieres añadir todos los archivos modificados o nuevos:

```sh
git add .
```

### 🔹 3. Hacer un commit
Después de agregar los archivos al área de staging, confirma los cambios con un mensaje descriptivo:

```sh
git commit -m "Descripción de los cambios"
```
### 🔹 4. Ver el historial de commits
Si quieres ver los commits anteriores en el repositorio:

```sh
git log
```
Si prefieres un historial más limpio con un resumen de cada commit:

```sh
git log --online
```

### 🔹 5. Deshacer cambios
👉 Revertir cambios no agregados a staging
Si has editado un archivo pero quieres restaurarlo antes de hacer git add:

```sh
git checkout -- nombre-del-archivo
```

👉 Eliminar cambios en staging
Si ya hiciste `git add` pero no quieres incluir el archivo en el commit:

```sh
git reset nombre-del-archivo
```

Si quieres sacar todos los archivos de staging:

```sh
git reset
```
👉 Deshacer un commit
Si quieres deshacer el último commit sin borrar los cambios:

```sh
git reset --soft HEAD~1
```
Si quieres deshacer el commit y borrar los cambios completamente:

```sh
git reset --hard HEAD~1
```

# ‼️🚨 6. Crear y gestionar ramas🚨‼️
Las ramas permiten trabajar en nuevas funcionalidades sin afectar el código principal.

👉 Ver las ramas existentes

```sh
git branch
```
👉 Crear una nueva rama
```
git checkout nombre-de-la-rama
```
👉 Cambiar de rama
```sh
git checkout nombre-de-la-rama
```
O puedes crear y cambiar a la nueva rama directamente con:
```sh
git checkout -b nombre-de-la-rama
```

### 🔹 8. Clonar un repositorio
Si quieres descargar un repositorio desde GitHub a tu computadora:

```sh
git clone https://github.com/usuario/repositorio.git
```
### 🔹 9. Descargar cambios del repositorio remoto
Si quieres actualizar tu repositorio local con los cambios más recientes del remoto:

```sh
git pull origin main
```
### 🔹 10. Subir cambios al repositorio remoto
Para subir los commits locales al repositorio en GitHub:

```sh
git push origin main
```
Si estás trabajando en otra rama:

```sh
git push origin nombre-de-la-rama
```

# 🤝 Colaborando en un Proyecto de GitHub

 ### 🔹 1. Clonar el repositorio
Si quieres contribuir a un proyecto, primero clónalo a tu computadora:

```sh
git clone https://github.com/usuario/repositorio.git
```
### 🔹 2. Crear una nueva rama para trabajar
Es recomendable crear una rama separada en lugar de trabajar en main directamente:

```sh
git checkout -b mi-nueva-rama
```
### 🔹 3. Hacer cambios y subirlos
Después de modificar archivos, agrégalos al área de staging, haz commit y súbelos al repositorio:

```sh
git add .
git commit -m "Agregué una nueva funcionalidad 🚀"
git push origin mi-nueva-rama
```
### 🔹 4. Crear un Pull Request en GitHub
Una vez que los cambios estén en GitHub, sigue estos pasos:

### 1. Ve a GitHub y abre el repositorio.
### 2. Verás un mensaje para crear un Pull Request (PR).
### 3. Asegúrate de comparar tu rama con `main y revisa los cambios.
### 4. Escribe un buen título y descripción explicando qué mejoras has hecho.
### 5. Envía el PR para que otros lo revisen.


### 🔥 Consejos Pro de GitHub
#### ✅ Usa un archivo .gitignore para evitar subir archivos innecesarios.
#### ✅ Escribe mensajes de commit claros y descriptivos.
#### ✅ Usa git stash si necesitas guardar cambios sin hacer commit.
#### ✅ Habilita GitHub Actions para automatizar tareas en el repositorio.
#### ✅ Aprende a usar forks y issues para colaborar en proyectos open-source.



