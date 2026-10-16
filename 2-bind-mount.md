# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO
docker run -d --name nginx-practica1 -p 8080:80 --mount "type=bind,source=C:\docker\nginx\html,target=/usr/share/nginx/html" nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?
#### Al ingresar al servidor Nginx se muestra el error 403 Forbidden debido a que  carpeta del equipo montada en /usr/share/nginx/html está vacía y no contiene un archivo index.html que la imagen Nginx pueda mostrar.

### ¿Qué pasa con el archivo index.html del contenedor?
#### El archivo index.html original del contenedor queda  d emanera oculta  por el bind mount, ya que la carpeta del equipo se monta sobre el directorio web de Nginx. El archivo original no se elimina, pero deja de ser visible mientras el montaje esté activo.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html

### ¿Qué sucede al ingresar al servidor de nginx?
#### Al ingresar al servidor Nginx se muestra la página web de la plantilla descargada de HTML5 UP debido que sus archivos se encuentran en el directorio del equipo vinculado al contenedor mediante el bind mount.

### Eliminar el contenedor
#### docker rm -f nginx-practica1

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
#### La plantilla descargada se vuelve a visualizar porque los archivos permanecen en el equipo y al crear otro contenedor montando la misma carpeta, Nginx puede acceder nuevamente a esos archivos.


