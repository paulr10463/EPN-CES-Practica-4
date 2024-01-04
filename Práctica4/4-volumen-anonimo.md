# Volúmenes
## ANÓNIMO
Un volumen anónimo es aquel que no posee un nombre específico y que Docker genera automáticamente al ejecutar un contenedor. Para crear un volumen anónimo, se utiliza la opción -v con solo la ruta del contenedor, sin necesidad de especificar la ruta del host

```
docker run -d --name server-nginx -v /usr/share/nginx/html -p 9800:80 nginx:alpine
```

### Para eliminar el contenedor y el volumen
Para eliminar el contenedor y el volumen anónimo, se puede usar el comando docker rm con las opciones -f y -v y el nombre del contenedor.
```
docker rm -fv server-nginx
```

_esta instrucción elimina el volumen si éste es de tipo anónimo_
