
---

### Cómo usar Docker para servir mi aplicación web localmente (como XAMPP)

Usar **Docker** para servir tu aplicación web localmente, similar a como lo harías con **XAMPP**, pero utilizando contenedores. 
#### Paso 1: Crear un Dockerfile

Lo primero fue crear un archivo **Dockerfile** en la carpeta de mi proyecto. Este archivo contiene las instrucciones necesarias para crear la imagen Docker, que incluirá todos los archivos de mi aplicación y el servidor web (en este caso **Nginx**) que los servirá.

Mi **Dockerfile** se ve así:

```dockerfile
# Usar una imagen base de Nginx
FROM nginx:alpine

# Copiar los archivos HTML, CSS, JS y cualquier otro archivo necesario al contenedor
COPY ./index.html /usr/share/nginx/html/index.html
COPY ./style.css /usr/share/nginx/html/style.css
COPY ./index.js /usr/share/nginx/html/index.js
COPY ./key.js /usr/share/nginx/html/key.js
COPY ./star-icon.svg /usr/share/nginx/html/star-icon.svg

# Si tienes una carpeta assets con imágenes o archivos adicionales, copiarla también
COPY ./assets /usr/share/nginx/html/assets

# Exponer el puerto 80 para que se pueda acceder desde fuera
EXPOSE 80
```

- **`FROM nginx:alpine`**: Esto usa una imagen base de Nginx, que es ligera y perfecta para servir contenido web.
- **`COPY`**: Aquí estoy copiando mis archivos locales (HTML, CSS, JS, imágenes, etc.) dentro del contenedor, específicamente a la carpeta donde Nginx los espera: `/usr/share/nginx/html/`.
- **`EXPOSE 80`**: Este comando expone el puerto 80, que es donde Nginx estará escuchando.

#### Paso 2: Construir la imagen de Docker

Una vez que tenía mi **Dockerfile** configurado, lo siguiente fue construir la imagen de Docker con este comando:

```bash
docker build -t movie-app .
```

- **`-t movie-app`**: Esto le da un nombre a la imagen (en este caso `movie-app`).
- El `.` al final le dice a Docker que el **Dockerfile** está en el directorio actual.

#### Paso 3: Ejecutar el contenedor

Después de construir la imagen, el siguiente paso es ejecutar el contenedor para que mi aplicación web esté disponible localmente. Lo hice con el siguiente comando:

```bash
docker run -d -p 8080:80 movie-app
```

- **`-d`**: Esto ejecuta el contenedor en segundo plano (modo "detached").
- **`-p 8080:80`**: Aquí estoy mapeando el puerto 80 dentro del contenedor al puerto 8080 de mi máquina local. Esto significa que podré acceder a mi aplicación en `http://localhost:8080`.
- **`movie-app`**: Este es el nombre de la imagen que creé en el paso anterior.

#### Paso 4: Verificar en el navegador

Una vez que el contenedor estaba en ejecución, abrí mi navegador y fui a:

```
http://localhost:8080
```

¡Y allí estaba! Mi aplicación web cargó correctamente, servida por Nginx a través de Docker.

#### Paso 5: Solucionar problemas (por ejemplo, error 403)

Si alguna vez me encontré con un error como **403 Forbidden** (lo cual suele pasar cuando los archivos no tienen los permisos adecuados), lo resolví de la siguiente manera:

1. **Accedí al contenedor** con:

   ```bash
   docker exec -it <container_id> sh
   ```

2. Cambié los permisos de los archivos con el siguiente comando para asegurarme de que Nginx pudiera acceder a ellos:

   ```bash
   chmod -R 755 /usr/share/nginx/html
   ```

3. También cambié la propiedad de los archivos para que Nginx pudiera usarlos, con el siguiente comando:

   ```bash
   chown -R nginx:nginx /usr/share/nginx/html
   ```

4. Luego, reinicié el contenedor con:

   ```bash
   docker restart <container_id>
   ```

#### Paso 6: Acceso desde otros dispositivos en la misma red

Si quiero que otras personas de la misma red local accedan a mi aplicación, solo necesito saber la **dirección IP local** de mi máquina.

- **En macOS** o **Linux** ejecuté:

  ```bash
  ifconfig
  ```

- **En Windows** ejecuté:

  ```bash
  ipconfig
  ```

Con la dirección IP local de mi máquina, otras personas en la misma red pueden acceder a la aplicación usando:

```
http://<tu_ip_local>:8080
```

#### Paso 7: Eliminar contenedores e imágenes viejas

Si alguna vez necesito limpiar contenedores e imágenes viejas, utilizo estos comandos:

- Para detener un contenedor:

  ```bash
  docker stop <container_id>
  ```

- Para eliminar un contenedor:

  ```bash
  docker rm <container_id>
  ```

- Para eliminar una imagen:

  ```bash
  docker rmi <image_id>
  ```


--- 
