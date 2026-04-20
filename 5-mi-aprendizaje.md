
## 1. IMÁGENES EN DOCKER
Las imágenes son plantillas de solo lectura usadas para crear contenedores.
### Descargar imágenes:
docker pull <imagen>
docker pull <imagen>:<tag>
###Ejemplos:
docker pull stirlingtools/stirling-pdf
docker pull stirlingtools/stirling-pdf:alpha
docker pull hello-world
docker pull nginx:alpine-perl
### Listar imágenes:
docker images
 ### Inspeccionar una imagen:
docker inspect <imagen>
docker inspect <imagen>:<tag>
 ### Generación del ID:
Se utiliza el algoritmo SHA-256 (hash criptográfico).
### Filtrar imágenes:
docker images | grep <termino>
### Eliminar imágenes:
docker rmi <imagen>:<tag>
docker rmi -f <imagen>
### Consideraciones:
- No elimina contenedores existentes.
- Se recomienda eliminar contenedores antes que imágenes.
## 2. CONTENEDORES
Los contenedores son instancias en ejecución de una imagen.
### Crear contenedor (sin ejecutar):
docker create --name <nombre> <imagen>:<tag>
### Iniciar contenedor:
docker start <nombre>
Crear y ejecutar directamente:
docker run --name <nombre> <imagen>:<tag>
Nota:
Si se ejecuta sin -d, el contenedor bloquea la terminal.
Ejecutar en segundo plano:
docker run -d --name <nombre> <imagen>:<tag>
### Listar contenedores:
docker ps        (en ejecución)
docker ps -a     (todos)
### Detener contenedor:
docker stop <nombre>
### Eliminar contenedor:
docker rm <nombre>
docker rm -f <nombre>
### Inspeccionar contenedor:
docker inspect <nombre>
## 3. MAPEO DE PUERTOS
Permite acceder a servicios del contenedor desde el host.
### Mapear puertos:
docker run -d -p <host>:<contenedor> <imagen>
### Ejemplo:
docker run -d -p 3000:80 nginx:alpine-perl
### Mapear múltiples puertos:
docker run -d -p 3000:80 -p 3001:80 <imagen>
### Forma semántica:
docker run --publish published=3000,target=80 <imagen>
### Publicar puertos automáticamente:
docker run -P -d <imagen>
### Importante:
El mapeo de puertos solo se define al crear el contenedor.
## 4. OPERACIONES CON CONTENEDORES
### Ejecutar comandos dentro de un contenedor:
docker exec <contenedor> <comando>
### Ejemplo:
docker exec jenkins ls -l
### Comandos:
ls    -> lista archivos
ls -l -> lista detallada (permisos, tamaño, fecha)
### Shell interactivo:
### Solo entrada:
docker exec -i <contenedor> bash
### Interactivo completo:
docker exec -it <contenedor> bash
### Diferencias:
-i -> mantiene entrada abierta
-t -> asigna terminal interactivo
