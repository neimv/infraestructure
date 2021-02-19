# Mini-Infraestructutra para analitica

Se crea infraestructura simple y pequeña para analitica, los servicios que contiene son:

- Postgresql con postgis, puerto:5432
- PGAdmin4, puerto: 5050
- jupyter notebook, puerto: 8888, con los siguientes lenguajes:
    * Python con pyspark, contine librerias para conectarse a los servicios que tiene el docker-compose, como presto, mongo y/o postgresql, aparte de librerias geospaciales
    * R
    * Scala con spark
- RabbitMQ con entorno web, puerto web: 15672, puerto: 5672
- Mongodb, puerto: 27017
- Mongo-express, interfaz web de administración, puerto: 8081
- Presto, interfaz de administración web puerto: 9090
- Redis, puerto: 6379
- Airflow (solo de desarrollo), puerto web: 8080

## Instrucciones de uso y acceso

Para ejecutar toda la mini infraestructura ser requiere de tener las siguientes variables de entorno:

> AWS_ACCESS_KEY_ID={access_key}
> AWS_SECRET_KEY={secret_key}
> AWS_SECRET_ACCESS_KEY={secret_key}
> estos son para el acceso a pgadmin
> email={email}
> analitica_pass={pass}

se pueden configurar en Linux/Mac en consola ejecutando o agregando al ~/.bashrc o ~/.zshrc, dependiendo del shell que se use:

`export AWS_ACCESS_KEY_ID={access_key}`
`export AWS_SECRET_KEY={secret_key}`
`export AWS_SECRET_ACCESS_KEY={secret_key}`
`export email={email}`
`export analitica_pass={pass}`

en windows:

`SET AWS_ACCESS_KEY_ID={access_key}`
`SET AWS_SECRET_KEY={secret_key}`
`SET AWS_SECRET_ACCESS_KEY={secret_key}`
`SET email={email}`
`SET analitica_pass={pass}`

para ejecutar los servicios se siguen los siguientes pasos:

1. `docker-compose up airflow-init`
2. `docker-compose up`

para mayores referencias se puede ver la documentación del docker de [airflow](https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html)

Para ejecutar un query en presto en consola se puede por medio de:

`docker exec -it presto presto --catalog hive`

presto esta conectado a hive de s3 por eso requiere las credenciales de AWS
