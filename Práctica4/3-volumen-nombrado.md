# Volúmenes
## NOMBRADO

### Crear volumen

```
docker volume create vol-postgres
```
### ¿Cuál es el Mountpoint de vol-postgres?
El punto de montaje (Mountpoint) del volumen llamado "vol-postgres" es la ubicación en el host donde se guardan los datos asociados con dicho volumen. Para determinar el Mountpoint de un volumen, se puede emplear el comando "docker volume inspect". En nuestro caso, utilizamos:
```
docker volume inspect vol-postgres
```
Asi, se mostrará la siguiente información
```
[
    {
        "CreatedAt": "2024-01-04T03:30:54Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/vol-postgres/_data",
        "Name": "vol-postgres",
        "Options": null,
        "Scope": "local"
    }
]
```
### ¿Cómo acceder a ese Mountpoint?
Para acceder al Mountpoint observado en el paso previo, se usa el comando cd para cambiar de directorio. 
Así, se emplea
```
cd /var/lib/docker/volumes/vol-postgres/_data
```
Este paso nos conducirá al directorio donde los datos del volumen están almacenados, permitiéndonos visualizar los archivos y directorios relacionados con la base de datos PostgreSQL que está siendo utilizada en el contenedor.

### Crear una red para postgres

```
docker network create postgres-net
```

### Servidor postgres usando el volumen nombrado

```
docker run -d --name server-postgres -e POSTGRES_DB=postgres-db -e POSTGRES_PASSWORD=P@ssw0rd -e POSTGRES_USER=user_01 -v vol-postgres:/var/lib/postgresql/data --network postgres-net postgres
```

### ¿Qué ha sucedido en vol-postgres?
Al instanciar el contenedor de PostgreSQL utilizando el volumen llamado "vol-postgres", se ha realizado la inicialización de la base de datos en el directorio /var/lib/postgresql/data del contenedor. Este directorio ha sido sincronizado con el directorio correspondiente al punto de montaje del volumen en el host. 

Esta sincronización implica que los datos de la base de datos se almacenan tanto en el contenedor como en el host, y cualquier modificación realizada en uno de ellos se reflejará en el otro. Esta configuración brinda persistencia de información incluso si el contenedor es eliminado dado que no está vinculado al ciclo de vida del contenedor.