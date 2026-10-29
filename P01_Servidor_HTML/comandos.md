# Documentación Práctica Docker - Nginx Alpine

## FASE 0 - Preparación

sudo apt update && sudo apt install -y git curl
git clone "repositorio"


## FASE 1 - Descargar Nginx:alpine

docker pull nginx:alpine
docker images


## FASE 2 - Crear contenedor

docker create --name alpine-server -it -p 8080:80 nginx:alpine 


## FASE 3 - Levantar y comprobar

docker start alpine-server
curl localhost:8080


## FASE 4 - Copiar página web


docker cp ./html/index.html alpine-server:/usr/share/nginx/html


## FASE 5 - Permisos en el contenedor

docker exec -it alpine-server sh

# Dentro del contenedor:
chown -R root:root /usr/share/nginx/html
find /usr/share/nginx/html -type d -exec chmod 755 {} \;
find /usr/share/nginx/html -type f -exec chmod 644 {} \;
exit


## FASE 6 - Monitoreo de logs

docker logs -f alpine-server


## FASE 7 - Crear imagen propia

docker container commit alpine-server javsolsal/imagen-alpine:v1


## FASE 8 - Exportar imagen a TAR

docker image save -o alpine-server.tar javsolsal/imagen-alpine:v1


## FASE 9 - Eliminar entorno local

docker stop alpine-server
docker rm alpine-server
docker rmi javsolsal/imagen-alpine:v1 


## FASE 10 - Importar y levantar servicio

docker image load -i alpine-server.tar
docker run -d -p 8080:80 --name alpine-server javsolsal/imagen-alpine:v1





 






