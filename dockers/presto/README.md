# PRESTO

### Correr el servidor de presto

Para correr el docker solo se requiere de crear la imagen y correrla

```bash
docker build -f Dockerfile -t presto --build-arg PRESTO_VERSION={version} .
```

```bash
docker run -p 8080:8080 --name presto presto
```

Espera las siguientes lineas:
```
INFO	main	io.prestosql.server.PrestoServer	======== SERVER STARTED ========
```

El servidor de presto estara en `localhost:8080` (the default port).

### Correr CLI

Para acceder a la interfaz y usar las particiones de hive (s3)

```bash
docker exec -it {container_name} presto --catalog hive
```

### Ejecutar Query 

Para ejecutar únicamente una query puede utilizar la variable de entorno QUERY para pasar la consulta

```
    docker run --env "QUERY=SELECT * FROM UNNEST(SEQUENCE(0, 100));" presto
```

Si la QUERY es un SELECT el resultado se verá escrito los logs del contendor

### Incremento de memoria 

#### Jvm

Para incrementar memoria de jvm es necesario agregar una mayor cantidad a la propiedad -Xmx el archivo [jvm.config](./default/etc/jvm.config)
