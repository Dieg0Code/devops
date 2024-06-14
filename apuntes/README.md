# Apuntes sobre DevOps

## Introducción

Normalmente existen dos equipos en las empresas de TI, el **equipo de desarrollo**, que se encarga de crear nuevas funcionalidades y desarrollar software, y el **equipo de infraestructura**, que se encarga de mantener los servidores y la infraestructura de la empresa. El **DevOps** es una metodología que busca unificar estos dos equipos, de manera que el desarrollo y la infraestructura se coordinen y trabajen juntos.

El equipo de desarrollo crea el productos y el equipo de infraestructura se encarga de velar que la infraestructura que mantiene el producto esté disponible 24/7 y sea escalable.

Esta separación entre los dos equipos suele traer algunos problemas como:

Para el equipo de desarrollo:

- Aislamiento entre los equipos.
- Fricciones entre los equipos.
- Uso de correo por sobre comunicación ágil.
- Baja automatización.

Para el equipo de infraestructura:

- Scripts rudimentarios.
- Calendarios de releases fijos.
- Puesta en producción mas lenta.

## ¿Qué es DevOps, cuál es su ciclo de vida y que beneficios aporta?

DevOps es la unión entre personas, procesos y tecnología, con el fin de proporcionar valor **continuamente** a los clientes. Los principales objetivos de DevOps son una **mayor calidad**, **menor tiempo de comercialización** y un **menor costo de implementación**. 

Implementar esta cultura nos trae beneficios como:

- Mejores objetivos comerciales.
- Mayor satisfacción del cliente.
- Agilidad en las entregas y alto rendimiento.
- Mejores productos.
- Armonía entre los equipos.
- Menos problemas en producción.
- Facilidad en el diagnostico y la resolución de incidentes.

### Ciclo de vida de DevOps

El ciclo de vida de DevOps consta de 8 etapas:

1. **Plan**: En esta etapa se definen los objetivos y se planifica el trabajo.
2. **Code**: En esta etapa se desarrolla el código.
3. **Build**: En esta etapa se compila el código.
4. **Test**: En esta etapa se prueban los cambios.
5. **Release**: En esta etapa se implementan los cambios.
6. **Deploy**: En esta etapa se despliegan los cambios.
7. **Operate**: En esta etapa se verifica que el sistema esté funcionando correctamente.
8. **Monitor**: En esta etapa se monitorea el sistema para detectar posibles problemas.

Esto se repite continuamente, de manera que se pueda mejorar el producto de manera iterativa.

### Aspectos Fundamentales de DevOps

- **Control de versiones**: git, svn, Github, GitLab, Bitbucket, Mercurial.
- **Integración continua**: Pipelines, Jenkins, automatizar compilaciones y pruebas cuando se hace commit.
- **Entrega continua**: Suministro de software rápido y confiable en cualquier momento.
- **Infraestructura como código**: Terraform. Definición declarativa de la infraestructura mediante archivos de definición basados en texto. Para revertir, desmontar y recrear entornos complejos.
- **Supervision y registro**: Prometheus, Grafana. Monitorización, recopilación  de métricas y vinculación de datos de performance.
- **Aprendizaje validado**: Análisis de datos para mejorar los procesos en cada ciclo nuevo.

## Docker

Docker es una plataforma de código abierto que permite automatizar el despliegue de aplicaciones dentro de contenedores de software. Estos contenedores son ligeros y portables, y garantizan que el software se ejecute de la misma manera en cualquier lugar.

El **Docker engine** es una tecnología que permite la creación y administración de contenedores funciona como una capa intermedia entre el sistema operativo y las aplicaciones.

Podemos virtualizer cualquier sistema operativo o aplicación en un contenedor Docker, lo que nos permite tener un entorno de desarrollo aislado y portable.

Conceptos importantes de Docker:

- **Contenedores**: Unidad de software que empaqueta el código y todas las dependencias necesarias de una aplicación.
- **Imágenes**: Paquete ligero y ejecutable de software con todo lo necesario para la aplicación.
- **Docker Engine**: Motor de ejecución de contenedores.
- **Podman**: Alternativa a Docker.
- **Docker Hub**: Repositorio de imágenes de Docker.
- **Docker compose**: Orquestador ligero de contenedores.
- **Docker Swarm**: Orquestador de contenedores, permite manejar un cluster.
- **Kubernetes**: Sistema para la administración de clusters y orquestación empresarial de contenedores.

### Comunicación externa e interna en un entorno de contenedores, mapeo de puertos

Los contenedores Docker pueden comunicarse entre sí a través de una red interna, pero para que un contenedor pueda comunicarse con el exterior, es necesario mapear los puertos del contenedor a los puertos del host. Esto se hace con el comando `-p` de Docker. Por ejemplo, si queremos mapear el puerto 80 del contenedor al puerto 8080 del host, podemos hacerlo con el siguiente comando:

```bash
docker run -p 8080:80 nombre_imagen
```

De esta manera, si accedemos a `http://localhost:8080` en el host, estaremos accediendo al puerto 80 del contenedor.

Docker internamente maneja una red mediante la cual los contenedores pueden comunicarse entre sí, los contenedores pueden estar todos en la misma red o podemos segmentarlos en diferentes redes para aislar ciertos servicios que nos interesen.

### Arquitectura interna de Docker Engine, CLI, Desktop y Compose

- **Docker Engine**: Es el motor de ejecución de contenedores de Docker. Es una tecnología que permite la creación y administración de contenedores y funciona como una capa intermedia entre el sistema operativo y las aplicaciones.
- **Docker CLI**: Es la interfaz de línea de comandos de Docker. Permite a los usuarios interactuar con el motor de Docker y realizar tareas como crear, ejecutar y administrar contenedores.
- **Docker Desktop**: Es una aplicación de escritorio que facilita la creación y administración de contenedores de Docker en sistemas operativos Windows y macOS.
- **Docker Compose**: Es una herramienta que permite definir y ejecutar aplicaciones Docker multi-contenedor. Permite definir la configuración de una aplicación en un archivo YAML y luego ejecutarla con un solo comando.


### Principales comando de Docker

- `docker run`: Crea y ejecuta un contenedor.
- `docker start <container>`: Inicia un contenedor detenido.
- `docker ps -a`: Muestra los contenedores en ejecución.
- `docker images -a`: Muestra las imágenes disponibles.
- `docker build -t <nombre_imagen> .`: Construye una imagen a partir de un Dockerfile.
- `docker pull <nombre_imagen>`: Descarga una imagen de Docker Hub.
- `docker push <nombre_imagen>`: Sube una imagen a Docker Hub.
- `docker exec -it <container> bash`: Ejecuta un comando en un contenedor en ejecución.
- `docker stop <container>`: Detiene un contenedor.
- `docker rm <container>`: Elimina un contenedor.
- `docker rmi <imagen>`: Elimina una imagen.
- `docker logs <container>`: Muestra los logs de un contenedor.
- `docker inspect <container>`: Muestra información detallada de un contenedor.


Por ejemplo, podemos ejecutar un contenedor desde docker Hub con el siguiente comando:

```bash
docker run -p 8080:80 -p  7080:7080 --name contBilling sotobotero/billingapp
```

Este comando crea un contenedor a partir de la imagen `sotobotero/billingapp` y lo ejecuta en el puerto 80 del contenedor y en el puerto 8080 del host. El contenedor se llama `contBilling`. Tiene dos puertos porque la aplicación internamente tiene dos servicios, el frontend y el backend.

### Docker Hub

Docker Hub es un servicio en la nube que permite a los desarrolladores compartir y almacenar imágenes de Docker. Cuenta con una gran cantidad de imágenes públicas que se pueden descargar y utilizar de forma gratuita, como bases de datos, servidores web, sistemas operativos, etc.

Además, Docker Hub permite a los desarrolladores almacenar sus propias imágenes de Docker de forma privada, lo que les permite compartir y colaborar en proyectos de forma segura.

Dependiendo de la imagen tienen diferentes versiones y configuraciones necesarias para su ejecución, por ejemplo una imagen de una Base de datos PostgreSQL necesita las siguientes configuraciones:

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -e POSTGRES_USER=postgres -e POSTGRES_DB=mydb -d postgres
```

En donde debemos configurar el usuario, la contraseña, la base de datos que se va a utilizar entre otras configuraciones que se pueden llegar a necesitar. En Docker Hub podemos encontrar la documentación necesaria para la ejecución de cada imagen así que es necesario consultar esta documentación para configurar optimate las imágenes según lo necesitemos.

También es importante mencionar que las imágenes tienen versiones como por ejemplo `postgres:13`, `postgres:12` o `postgres:latest`, en donde `latest` es la versión más reciente de la imagen. Esta versión no es muy recomendable usarla ya que puede tener cambios que no esperamos y que pueden afectar el funcionamiento de nuestra aplicación, es mas seguro usar una versión especifica para no encontrarnos con sorpresas.

### Como Dockerizar una aplicación

Docker es una herramienta que nos permite empaquetar una aplicación y todas sus dependencias en un contenedor, de manera que la aplicación se ejecute de la misma manera en cualquier lugar que tenga Docker instalado. Antiguamente solía ocurrir el problema de que la máquina que desarrolló cierta aplicación tenía una configuración especifica ya sea de sistema operativo, librerías, versiones de software, etc. y al momento de querer ejecutar esta aplicación en otra máquina con una configuración diferente, la aplicación no funcionaba correctamente.

Docker soluciona este problema empaquetando la aplicación con todas sus dependencias especificas en un contenedor, hace uso de unos archivos llamados `Dockerfile` que contienen las instrucciones necesarias para construir una imagen de Docker, es en cierto modo una especie de receta en la que se especifican todos los ingredientes y pasos necesarios para construir la imagen.

Por ejemplo:

```Dockerfile
FROM nginx:stable-alpine

VOLUME /tmp

# Intala la aplicación web en el servidor nginx
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY dist/billingApp /usr/share/nginx/html
COPY mime.types /etc/nginx/mime.types

# Instala OpenJDK 17
RUN apk --no-cache add openjdk17-jre
# Definimos la variable de entorno JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-17-openjdk
ENV PATH $JAVA_HOME/bin:$PATH

# Verificamos la instalación de Java
RUN java -version

# Instala el microservicio de java
ENV JAVA_OPTS=""
ARG JAR_FILE
ADD ${JAR_FILE} app.jar

# Copiamos el script de inicialización
COPY appshell.sh appshell.sh

# Puerto 7080 para el backend y el 80 para la aplicación web
EXPOSE 80 7080

ENTRYPOINT [ "sh", "/appshell.sh" ]
```

En este archivo se especifica que se va a usar una imagen de `nginx` estable con Alpine, se copian los archivos necesarios para la aplicación web, se instala OpenJDK 17, se copia el archivo `.jar` del microservicio, se copia un script de inicialización y se exponen los puertos 80 y 7080.

El script de inicialización `appshell.sh` es el siguiente:

```bash
#!/bin/bash

# Start the java app
java -jar /app.jar &
status=$?
if [ $status -ne 0 ]; then
  echo "Failed to start java microservice: $status"
  exit $status
fi
# Start the second process (nginx server)
nginx &
status=$?
if [ $status -ne 0 ]; then
  echo "Failed to start nginx process: $status"
  exit $status
fi

# Naive check runs checks once a minute to see if either of the processes exited.
# This illustrates part of the heavy lifting you need to do if you want to run
# more than one service in a container. The container exits with an error
# if it detects that either of the processes has exited.
# Otherwise it loops forever, waking up every 60 seconds

while sleep 60; do
  ps aux |grep app.jar |grep -q -v grep
  PROCESS_1_STATUS=$?
  ps aux |grep nginx |grep -q -v grep
  PROCESS_2_STATUS=$?
  # If the greps above find anything, they exit with 0 status
  # If they are not both 0, then something is wrong
  if [ $PROCESS_1_STATUS -ne 0 -o $PROCESS_2_STATUS -ne 0 ]; then
    echo "One of the processes has already exited."
    exit 1
  fi
done
```

En donde:

- Se inicia el microservicio de Java.
- Se inicia el servidor Nginx.
- Se verifica que ambos procesos estén en ejecución.
- Si alguno de los procesos falla, se detiene el contenedor.

Para construir la imagen de Docker a partir de este `Dockerfile` se ejecuta el siguiente comando:

```bash
docker build -t billingapp --no-cache --build-arg JAR_FILE=target/*.jar .
```

En donde `billingapp` es el nombre de la imagen y `--build-arg JAR_FILE=target/*.jar` es el argumento que se le pasa al `Dockerfile` para que pueda copiar el archivo `.jar` del microservicio.

Una vez construida la imagen, se puede ejecutar un contenedor a partir de ella con el siguiente comando:

```bash
docker run -p 8080:80 -p 7080:7080 --name contBilling billingapp
```

En donde `contBilling` es el nombre del contenedor y `billingapp` es el nombre de la imagen.

Podemos subir esta imagen a Docker Hub si queremos de la siguiente manera:

```bash
docker tag billingapp nombre_usuario/billingapp
docker push nombre_usuario/billingapp
```

Con usar Docker le estamos ahorrando al equipo de infraestructura todas las configuraciones necesarias para que la aplicación pueda ejecutarse en el servidor, como instalaciones de Java, Nginx, configuraciones de puertos, etc. Todo esto ya viene empaquetado en el contenedor de Docker.

## Docker Compose

En la aplicación que venimos trabajando empaquetamos tanto el frontend como el backend en un solo contenedor, pero lo normal es que cada servicio este separado en un contenedor propio, lo normal en esta aplicación sería tener un contenedor para el frontend, otro para el microservicio de Java, otro para la base de datos y otro para el DBMS o interfaz gráfica para administrar la base de datos.

Es en estos escenarios en donde una aplicación consta de varias partes en donde entran en juego los orquestados, estos son herramientas que nos permiten definir y ejecutar aplicaciones Docker multi-contenedor en donde los diferentes contenedores se comunican entre sí. Docker Compose es una de estas herramientas.

Los archivos de Docker Compose son archivos YAML que definen los servicios, las redes y los volúmenes de una aplicación multi-contenedor. Por ejemplo, el archivo `stack-billing.yml` para la aplicación que venimos trabajando sería algo así:

```yaml
version: '3.8'

services:
# database engine service
  postgres_db:
    container_name: postgres
    image: postgres:13
    restart: always
    ports:
      - 5432:5432
    volumes:
      - ./dbfiles:/docker-entrypoint-initdb.d
      - ./postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
# Adminer service
  adminer:
    container_name: adminer
    image: adminer
    restart: always
    depends_on:
      - postgres_db
    ports:
      - 9090:8080
```

En este archivo se definen dos servicios, uno para la base de datos PostgreSQL y otro para la interfaz gráfica de administración de la base de datos Adminer. Se definen los puertos, los volúmenes y las variables de entorno necesarias para cada servicio.

En `volume` se definen los volúmenes que se van a montar en el contenedor, en este caso se monta un volumen con los archivos de inicialización de la base de datos y otro con los datos de la base de datos.

```bash
#!/bin/bash
set -e

psql -v ON_ERROR_STOP=1 --username "$POSTGRES_USER" --dbname "$POSTGRES_DB" <<-EOSQL
    CREATE USER billingapp WITH PASSWORD 'qwerty';
    ALTER USER billingapp WITH SUPERUSER;
    CREATE DATABASE billingapp_db;
    GRANT ALL PRIVILEGES ON DATABASE billingapp_db TO billingapp;
    GRANT ALL ON SCHEMA public TO billingapp;
EOSQL
```

Este archivo se monta en el contenedor de la base de datos y se ejecuta al iniciar el contenedor, en este caso se crea un usuario y una base de datos para la aplicación.

Para ejecutar los servicios definidos en el archivo `stack-billing.yml` se ejecuta el siguiente comando:

```bash
docker compose -f stack-billing.yml up -d
```

En donde `-f` se usa para especificar el archivo de Docker Compose y `-d` se usa para ejecutar los servicios en segundo plano.

### Volúmenes en Docker y puertos

Los volúmenes en Docker son una forma de persistir los datos de un contenedor en el host. Los volúmenes son directorios que se montan en el contenedor y que permiten que los datos persistan incluso si el contenedor se elimina. Podemos montar un volumen en un contenedor con el comando `-v` de Docker. Por ejemplo, si queremos montar el directorio `/datos` del host en el directorio `/datos` del contenedor, podemos hacerlo con el siguiente comando:

```bash
docker run -v /datos:/datos nombre_imagen
```

Si es que queremos eliminar un contenedor que maneja la base de datos no nos interesa perder todos los datos que este contenedor tenía, es por eso que lo volúmenes se deben guardar en un directorio del host para que estos datos persistan. Un volumen es a fines prácticos es almacenamiento estático para los contenedores, se suelen usar para bases de datos, para logs, para montar archivos de configuración, etc.

Ejemplo:

- `Local filesystem path` `:` `container mount path`.
- `var/lib/postgresql/data:/var/lib/postgresql/data`: En este caso se monta el directorio `/var/lib/postgresql/data` del host en el directorio `/var/lib/postgresql/data` del contenedor.
- `/home/bds/postgres:/var/lib/postgresql/data`: En este caso se monta el directorio `/home/bds/postgres` del host en el directorio `/var/lib/postgresql/data` del contenedor.


Los puertos en Docker son una forma de exponer los servicios de un contenedor al exterior. Los puertos se pueden mapear con el comando `-p` de Docker. Por ejemplo, si queremos mapear el puerto 80 del contenedor al puerto 8080 del host, podemos hacerlo con el siguiente comando:

```bash
docker run -p 8080:80 nombre_imagen
```

De esta manera, si accedemos a `http://localhost:8080` en el host, estaremos accediendo al puerto 80 del contenedor.

### Separar los contenedores

Para separar los contenedores debemos escribir un archivo `Dockerfile` para cada servicio, por ejemplo, para el frontend:

```Dockerfile
FROM nginx:stable-alpine

VOLUME /tmp

RUN rm -rf /usr/share/nginx/html/*

COPY nginx.conf /etc/nginx/nginx.conf
COPY billingApp /usr/share/nginx/html
COPY mime.types /etc/nginx/mime.types

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

Y para el microservicio de Java:

```Dockerfile
# Usa una imagen base con JRE 17 en Alpine
FROM eclipse-temurin:17-alpine

# Create a new group with specific uid and non-root user called "admin"
# Be sure that group id are not present on host. if already exist change by arbitrary other uid
RUN addgroup -g 1028 devopsc \
    && adduser -D -G devopsc admin

# Create a new mount point at /tmp on native host because a volume is more efficient and faster than filesystem
VOLUME /tmp

# Copiamos el jar a la imagen
ARG JAR_FILE
# Establece una variable de entorno para la contraseña de la base de datos
ARG DB_PASSWORD

# Establece la variable de entorno DB_PASSWORD con el valor del argumento
ENV DB_PASSWORD=$DB_PASSWORD

# Copia el archivo JAR
COPY ${JAR_FILE} /tmp/app.jar

# Change ownership of the /app directory to the "admin" user
RUN chown -R admin:devopsc /tmp

# Cambia al usuario 'admin'
USER admin

# Ejecutamos el jar al iniciar el contenedor
ENTRYPOINT ["java","-jar","/tmp/app.jar"]
```

Ahora debemos actualizar el archivo de Docker Compose para que use estos nuevos `Dockerfile`:

```yaml
version: '3.8'

services:
# database engine service
  postgres_db:
    container_name: postgres
    image: postgres:13
    restart: always
    ports:
      - 5432:5432
    volumes:
      - ./dbfiles:/docker-entrypoint-initdb.d
      - ./postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: qwerty
      POSTGRES_DB: postgres
# Adminer service
  adminer:
    container_name: adminer
    image: adminer
    restart: always
    depends_on:
      - postgres_db
    ports:
      - 9090:8080

# Billing app backend service
  billingapp-back:
    build:
      context: ./java
      args:
        - JAR_FILE=*.jar
        - DB_PASSWORD=qwerty
    container_name: billingApp-back
    environment:
      - JAVA_OPTS=
        - Xms=256m
        - Xmx=256m
    depends_on:
      - postgres_db
    ports:
      - 8080:8080

# Billing app frontend service
  billingapp-front:
    build:
      context: ./angular
    container_name: billingApp-front
    depends_on:
      - billingapp-back
    ports:
      - 80:80
```

Con esto definimos los 4 servicios de la aplicación, la base de datos, la interfaz gráfica de administración de la base de datos, el frontend y el backend. Se definen los puertos, los volúmenes y las variables de entorno necesarias para cada servicio.

Para ejecutar los servicios definidos en el archivo `stack-billing.yml` se ejecuta el siguiente comando:

```bash
docker compose -f stack-billing.yml up -d
```

Con esto tenemos una aplicación multi-contenedor en la que cada servicio está separado en un contenedor propio.

### Como conectarse a un contenedor por SSH

Podemos conectarnos a un contenedor podemos ejecutar el siguiente comando:

```bash
docker exec -it nombre_contenedor sh
```

Con esto iniciado una shell en el contenedor con la cual podemos interactuar con el como lo haríamos con cualquier sistema operativo. Esto es útil para revisar logs, ejecutar comandos, instalar paquetes, etc.

### Limitar y monitorizar recursos físicos (RAM, CPU) deL host de los contenedores

Podemos limitar los recursos físicos de los contenedores con los siguientes comandos:

- `--memory`: Limita la cantidad de memoria RAM que puede usar el contenedor.
- `--cpus`: Limita la cantidad de CPUs que puede usar el contenedor.

Por ejemplo, si queremos limitar un contenedor a 1GB de RAM y 1 CPU, podemos hacerlo con el siguiente comando:

```bash
docker run --memory 1g --cpus 1 nombre_imagen
```

Para monitorizar los recursos físicos de los contenedores podemos usar herramientas como `docker stats` o `docker top`. Por ejemplo, si queremos ver las estadísticas de los contenedores en ejecución, podemos hacerlo con el siguiente comando:

```bash
docker stats
```

Este comando nos mostrará las estadísticas de los contenedores en ejecución, como el uso de CPU, memoria, red y disco.

También podemos configurar eso en el archivo yaml de docker compose:

```yaml
version: '3.1'

services:
#database engine service
  postgres_db:
    container_name: postgres
    image: postgres:latest
    restart: always
    ports:
      - 5432:5432
    volumes:
        #allow *.sql, *.sql.gz, or *.sh and is execute only if data directory is empty
      - ./dbfiles:/docker-entrypoint-initdb.d
      - /var/lib/postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: qwerty
      POSTGRES_DB: postgres    
#database admin service
  adminer:
    container_name: adminer
    image: adminer
    restart: always
    depends_on: 
      - postgres_db
    ports:
       - 9090:8080
#Billin app backend service
  billingapp-back:
    build:
      context: ./java
      args:
        - JAR_FILE=*.jar
        - DB_PASSWORD=qwerty
    container_name: billingApp-back      
    environment:
       - JAVA_OPTS=
         -Xms256M 
         -Xmx256M         
    depends_on:     
      - postgres_db
    ports:
      - 8080:8080 
#Billin app frontend service
  billingapp-front:
    build:
      context: ./angular 
    deploy:   
        resources:
           limits: 
              cpus: "0.15"
              memory: 250M
#recusos dedicados, mantiene los recursos disponibles del host para el contenedor
           reservations:
              cpus: "0.1"
              memory: 128M
    container_name: billingApp-front
    depends_on:     
      - billingapp-back
#rango de puertos para escalar    
    ports:
      - 80:80 
```

En donde podemos configurar también parámetros de despliegue como limites para el consumo de cpu y memoria, ademas de limitar la reserva que el contenedor puede hacer.

### Entornos virtuales

Una practica común en DevOps es manejar diferentes entornos virtuales para una aplicación, en un solo Host podemos tener entornos de desarrollo, pruebas y producción. Esto lo podemos conseguir mediante la segmentación de redes, docker nos permite manejar diferentes segmentos de red para cada entorno, un usuario puede diferenciar esto según el puerto que se exponga, por ejemplo, el puerto 80 para producción y el puerto 81 para preproducción.

Por ejemplo en un escenario en donde tenemos dos entornos, producción y preproducción en donde:

- Producción:
  - JRE: Java 18
  - Web server: Nginx 1.19
  - Base de datos: PostgreSQL 13.1, puerto 5432
  - Frontend: Angular 12, localhost:80
  - Backend: Java 18, localhost:8080
  - 172.16.235.0/24
- Preproducción
  - JRE: Java 18
  - Web server: Nginx 1.19
  - Base de datos: PostgreSQL 13.1, puerto 4432
  - Frontend: Angular 12, localhost:81
  - Backend: Java 18, localhost:7080
  - 172.16.232.0/24

Para configurar estos entornos debemos hacer algunas modificaciones en el archivo de Docker Compose, por ejemplo:

```yaml
version: '3.1'

services:
#database engine service
  postgres_db_prod:
    container_name: postgres_prod
    image: postgres:latest
    restart: always
    networks:
     - env_prod
    ports:
      - 5432:5432
    volumes:
        #allow *.sql, *.sql.gz, or *.sh and is execute only if data directory is empty
      - ./dbfiles:/docker-entrypoint-initdb.d
      - /var/lib/postgres_data_prod:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: qwerty
      POSTGRES_DB: postgres    


  postgres_db_prep:
    container_name: postgres_prep
    image: postgres:latest
    restart: always
    networks:
     - env_prep
    ports:
      - 4432:5432
    volumes:
        #allow *.sql, *.sql.gz, or *.sh and is execute only if data directory is empty
      - ./dbfiles:/docker-entrypoint-initdb.d
      - /var/lib/postgres_data_prep:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: qwerty
      POSTGRES_DB: postgres    

#database admin service
  adminer:
    container_name: adminer
    image: adminer
    restart: always
    depends_on: 
      - postgres_db_prod
      - postgres_db_prep
    networks:
     - env_prod
     - env_prep
    ports:
       - 9090:8080


#Billin app backend service
  billingapp-back-prod:
    build:
      context: ./java
      args:
        - JAR_FILE=billing-0.0.3-SNAPSHOT.jar
    container_name: billingApp-back-prod     
    environment:
       - JAVA_OPTS=
         -Xms256M 
         -Xmx256M         
    depends_on:     
      - postgres_db_prod
    networks:
     - env_prod
    ports:
      - 8080:8080 

#Billin app backend service
  billingapp-back-prep:
    build:
      context: ./java
      args:
        - JAR_FILE=billing-0.0.2-SNAPSHOT.jar
    container_name: billingApp-back-prep      
    environment:
       - JAVA_OPTS=
         -Xms256M 
         -Xmx256M         
    depends_on:     
      - postgres_db_prep
    networks:
     - env_prep
    ports:
      - 7080:7080 

#Billin app frontend service
  billingapp-front-prod:
    build:
      context: ./angular 
    deploy:   
        resources:
           limits: 
              cpus: "0.15"
              memory: 250M
#recusos dedicados, mantiene los recursos disponibles del host para el contenedor
           reservations:
              cpus: "0.1"
              memory: 128M
    #container_name: billingApp-front
    depends_on:     
      -  billingapp-back-prod
#rango de puertos para escalar   
    networks:
     - env_prod 
    ports:
      - 80:80 


#Billin app frontend service
  billingapp-front-prep:
    build:
      context: ./angular 
    deploy:   
        resources:
           limits: 
              cpus: "0.15"
              memory: 250M
#recusos dedicados, mantiene los recursos disponibles del host para el contenedor
           reservations:
              cpus: "0.1"
              memory: 128M
    #container_name: billingApp-front
    depends_on:     
      - billingapp-back-prep
#rango de puertos para escalar   
    networks:
     - env_prep 
    ports:
      - 81:81

networks:
  env_prod:
    driver: bridge  
    #activate ipv6
    driver_opts: 
            com.docker.network.enable_ipv6: "true"
    #IP Adress Manager
    ipam: 
        driver: default
        config:
        - 
          subnet: 172.16.232.0/24
          gateway: 172.16.232.1
        - 
          subnet: "2001:3974:3979::/64"
          gateway: "2001:3974:3979::1"


  env_prep:   
    driver: bridge  
    #activate ipv6
    driver_opts: 
            com.docker.network.enable_ipv6: "true"
    #IP Adress Manager
    ipam:
        driver: default
        config:
        - 
          subnet: 172.16.235.0/24
          gateway: 172.16.235.1
        - 
          subnet: "2001:3984:3989::/64"
          gateway: "2001:3984:3989::1"
```

En donde agregamos configuraciones nuevas como las redes `env_prod` y `env_prep` en donde se definen las subredes y las puertas de enlace para cada entorno, también se definen los servicios para cada entorno y se les asigna la red correspondiente.

## Docker Swarm
Docker Swarm es una herramienta de orquestación de contenedores que permite administrar un clúster de contenedores de Docker. Es en cierto sentido un intermedio entre docker compose y Kubernetes, es más sencillo que Kubernetes pero más potente que Docker Compose.

Kubernetes suele ser usado en entornos empresariales en donde se usa para manejar infraestructura como código, para manejar clusters y para orquestar microservicios, mientras que en entornos de pruebas lo mas común es que se trabaje con compose, sin embargo, también se puede trabajar con Swarm en entornos de pruebas.

A la hora de escoger que orquestador usar debemos considerar varios factores como el tamaño de la empresa, el presupuesto y la cantidad de contenedores, par soluciones pequeñas basta con compose, para una en donde se tengan que manejar mas de una máquina porque se administran varios servidores en un cluster y tenemos diferentes replicas de los servicios, tolerancia a fallos y alta disponibilidad pero el entorno sigue siendo pequeño, lo mejor es usar Swarm, para entornos mas grandes y complejos lo mejor es usar Kubernetes.

Para activar Docker Swarm se ejecuta el siguiente comando:

```bash
docker swarm init
```

Esto inicia un clúster de Docker Swarm y nos deja como el nodo líder del clúster.

Para obtener info sobre si docker swarm esta activo podemos ejecutar el comando:

```bash
docker info
```

En donde nos mostrara si está activo o no. Ademas nos muestra información relevante como la dirección IP de nuestro nodo, esto es relevante ya que si necesitamos probar luego nuestra aplicación debemos usar esta dirección ya que localhost no funcionara.

### Escalar contenedores con Swarm y definir parámetros de la orquestación

Para trabajar con Docker Swarm podemos usar el mismo archivo yaml que usábamos con compose, la diferencia es que con Swarm podemos agregar parámetros de orquestación, por ejemplo, escalar en numero de replicas de un servicio.

```yaml
version: '3.1'

services:
#database engine service
  postgres_db:
    #container_name: postgres
    image: postgres:latest
    restart: always
    ports:
      - 5432:5432
    volumes:
        #allow *.sql, *.sql.gz, or *.sh and is execute only if data directory is empty
      - ./dbfiles:/docker-entrypoint-initdb.d
      - /var/lib/postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: qwerty
      POSTGRES_DB: postgres    
#database admin service
  adminer:
    #container_name: adminer
    image: adminer
    restart: always
    depends_on: 
      - postgres_db
    ports:
       - 9090:8080


#Billin app backend service
  billingapp-back:
    build:
      context: ./java
      args:
        - JAR_FILE=*.jar
    image: billingapp_v2_billingapp-back:latest
    #container_name: billingApp-back      
    environment:
       - JAVA_OPTS=
         -Xms256M 
         -Xmx256M         
    depends_on:     
      - postgres_db
    ports:
      - 8080:8080 


#Billin app frontend service
  billingapp-front:
    build:
      context: ./angular
    image: billingapp_v2_billingapp-front 
    deploy: 
        replicas: 3
        resources:
           limits: 
              cpus: "0.15"
              memory: 250M
#recusos dedicados, mantiene los recursos disponibles del host para el contenedor
           reservations:
              cpus: "0.1"
              memory: 128M
    #container_name: billingApp-front
    depends_on:     
      - billingapp-back
#rango de puertos para escalar    
    ports:
      - 80-85:80 
```

En este archivo se define un servicio de frontend con 3 replicas, esto significa que se van a crear 3 contenedores con el servicio de frontend. Por lo general se definen mas replicas para servicios que se espera que tengan una alta demanda, como el frontend de una aplicación web. También con docker swarm es obligatorio que definamos la imagen que va a usar un contenedor.

En Docker Swarm las orquestaciones se conocen como `stack`, es por eso que cambia un poco el comando de despliegue.

```bash
docker stack deploy -c stack-billing.yml billing
```

Con esto se despliega la aplicación en el clúster de Docker Swarm.

Para listar los servicios que se están ejecutando en el clúster se ejecuta el siguiente comando:

```bash
docker service ls
```

Este comando nos mostrará una lista de los servicios que se están ejecutando en el clúster, con información como el nombre del servicio, el número de replicas, el estado, etc.

Para desactivar Docker Swarm se ejecuta el siguiente comando:

```bash
docker swarm leave --force
```

Con esto se desactiva el clúster de Docker Swarm y se vuelve al modo de ejecución normal de Docker.

También si queremos podemos eliminar el clúster con el siguiente comando:

```bash
docker stack rm billing
```

## Kubernetes

Kubernetes es una plataforma de orquestación de contenedores, es la mas usada actualmente en entornos empresariales, es una herramienta de código abierto que permite automatizar la implementación, el escalado y la administración de aplicaciones en contenedores. También existe OpenShift que es una versión de Kubernetes de Red Hat.

En escenarios en donde tenemos cientos o miles de contenedores, Kubernetes es la mejor opción ya que nos permite manejar la infraestructura como código, orquestar microservicios, manejar clusters, tolerancia a fallos, alta disponibilidad, etc.

### Escalabilidad vertical, horizontal y cluster

La escalabilidad es la capacidad de los sistemas para adaptarse al crecimiento, por demanda y complejidad.Por ejemplo supongamos que tenemos un sistema que fue diseñado para soportar una carga de trabajo de al menos 100 personas conectadas simultáneamente, supongamos que para soportar dicha carga de usuarios necesitamos 2 core de CPU y 4gb de RAM par que el sistema no se caiga y pueda funcionar correctamente con esa carga, si la carga no aumentara estos recursos seria suficientes, pero en la realidad esto no suele ser así, la carga de usuarios con el tiempo suele aumentar bastante, ademas también la complejidad del sistema suele aumentar por lo que las nuevas versiones van a necesitar mas recursos para seguir funcionando con normalidad, podemos llegar a duplicar los recursos necesarios en un principio, incluso mas. Cuando nos enfrentamos a esta situación tenemos que plantearnos como enfrentar ese problema de escalabilidad, vertical u horizontalmente.

El escalamiento vertical consiste en agregar más recursos al mismo nodo y con esto aumentar su poder de computo, por ejemplo, si tenemos un nodo con 2 core de CPU y 4gb de RAM y necesitamos mas recursos podemos agregar 2 core de CPU y 4gb de RAM mas, con esto el nodo tendría 4 core de CPU y 8gb de RAM, esto es lo que se conoce como escalamiento vertical.

Por otro lado el escalamiento horizontal consiste en agregar mas nodos con las mismas características y distribuir la carga de trabajo entre ellos, por ejemplo si tenemos un nodo con 2 core de CPU y 4gb de RAM y necesitamos mas recursos podemos agregar otro nodo con las mismas características, con esto tendríamos dos nodos con 2 core de CPU y 4gb de RAM cada uno, esto es lo que se conoce como escalamiento horizontal.

El escalamiento vertical tiene un límite, ya que no podemos agregar recursos infinitamente a un nodo, en algún momento llegaremos a un límite en el que no podremos seguir agregando mas recursos, por otro lado el escalamiento horizontal no tiene un límite, podemos agregar nodos infinitamente y distribuir la carga de trabajo entre ellos.

El escalamiento vertical es mas sencillo de implementar, ya que solo debemos agregar mas recursos al nodo, mientras que el escalamiento horizontal es mas complejo, ya que debemos distribuir la carga de trabajo entre los nodos y asegurarnos de que todos los nodos estén sincronizados, es aquí donde entra en juego Kubernetes.

## Principales características de Kubernetes

Kubernetes es una plataforma de orquestación de contenedores que nos permite escalar horizontalmente, es decir, agregar mas nodos al clúster y distribuir la carga de trabajo entre ellos. Kubernetes nos permite escalar de forma automática, es decir, si la carga de trabajo aumenta, Kubernetes puede agregar mas nodos al clúster y distribuir la carga de trabajo.

También es conocido como `K8`, esta inspirado en el sistema llamado `Borg` de Google, es un administrador de clusters capaz de operar cientos de miles de trabajos de miles de aplicaciones diferentes en varios clusters cada uno con hasta decenas de maquinas.

Principales características:

- Opensource: Kubernetes es un proyecto de código abierto, lo que significa que cualquiera puede contribuir al desarrollo de la plataforma.
- Auto-Sanado: Kubernetes es capaz de detectar y corregir errores automáticamente, por ejemplo, si un nodo falla, Kubernetes puede reiniciar los contenedores en otro nodo.
- Escalado Horizontal: Kubernetes es capaz de escalar horizontalmente, es decir, agregar mas nodos al clúster y distribuir la carga de trabajo entre ellos.
- Balanceo de carga y discovery: Kubernetes es capaz de distribuir la carga de trabajo entre los nodos y descubrir automáticamente los servicios en el clúster.
- Licencia Apache v2: Kubernetes es una plataforma de código abierto con licencia Apache v2, lo que significa que cualquiera puede usarla, modificarla y distribuirla libremente.
- Creado por Google en 2015: Kubernetes fue creado por Google en 2015 y es una de las plataformas de orquestación de contenedores mas populares del mundo.
- Escrito en Go: Kubernetes esta escrito en Go, un lenguaje de programación de código abierto desarrollado por Google.
- Mantenido por Cloud Native Computing Foundation (parte de la Linux Foundation): Kubernetes es mantenido por la Cloud Native Computing Foundation, una organización sin fines de lucro que promueve la adopción de tecnologías de código abierto en la nube.

## Arquitectura interna de un clúster de Kubernetes

Un cluster de Kubernetes se compone de varias máquinas llamadas Nodos, que se agrupan en **nodos maestros** y **nodos workers**. Los **nodos maestros** controlan el cluster y los **nodos workers** alojan los pods que son los componentes de carga de la aplicación.

### Nodos maestros

Los nodos maestros son los encargados de controlar el cluster, se componen de los siguientes componentes:

- **API Server**: Provee la interacción para las herramientas de administración de kubectl o el dashboard de Kubernetes.
- **Scheduler**: Es el encargado de asignar los pods a los nodos, es el componente que decide en que nodo se va a ejecutar un pod.
- **Controller Manager**: Supervisa controladores más pequeños que ejecutan tareas de replicar pods y maneja operaciones de los nodos.
- **etcd**: Es el almacén de datos del cluster, es el componente que se encarga de almacenar el estado del cluster.

### Nodos workers

Los nodos workers son los encargados de alojar los pods, se componen de los siguientes componentes:

- **Kubelet**: Es el agente que se ejecuta en cada nodo y se encarga de gestionar los pods.
- **Kube-proxy**: Es el encargado de gestionar el tráfico de red en el cluster, es el componente que se encarga de redirigir el tráfico de red a los pods.
- **Container Runtime**: Es el motor de contenedores que se ejecuta en cada nodo, es el componente que se encarga de ejecutar los contenedores.

### Tipos de Clusters de Kubernetes, gestionados, On-Premise y All-in-one

Existen varios tipos de clusters de Kubernetes, los mas comunes son:

- **On-Premise**: Son clusters que se ejecutan en un entorno local, es decir, en un centro de datos propio, en un servidor local o en una máquina virtual.
  - **All-in-one**: Se instala todo en un único nodo usando ``mini kube`` para pruebas y desarrollo.
  - **Single master and multiworker**: Un nodo para el control panel y uno o más nodos controlados por el nodo maestro.
  - **Single master, single etcd and multiworker**: Un nodo para el control panel, un nodo para almacenar la configuración y el estado y uno o más nodos controlados por el nodo maestro.
  - **Multi master and multiworker**: Múltiples nodos para el control panel en alta disponibilidad y uno o más nodos controlados por el master en HA (high availability).

- **Multi master, multi etcd and multiworker**: Múltiples nodos par el control panel, múltiples nodos para el almacenamiento etcd en alta disponibilidad y uno o más nodos controlados por el master en HA.

- **Gestionados**: Son clusters que se ejecutan en un entorno en la nube, es decir, en un proveedor de servicios en la nube como AWS, Azure o Google Cloud.
  - **GKE (Google Kubernetes Engine)**: Es un servicio de Google Cloud que permite ejecutar clusters de Kubernetes en la nube de Google.
  - **EKS (Amazon Elastic Kubernetes Service)**: Es un servicio de AWS que permite ejecutar clusters de Kubernetes en la nube de Amazon.
  - **AKS (Azure Kubernetes Service)**: Es un servicio de Azure que permite ejecutar clusters de Kubernetes en la nube de Microsoft.
  - **IBM Cloud Kubernetes Service**: Es un servicio de IBM Cloud que permite ejecutar clusters de Kubernetes en la nube de IBM.

### Objetos de Kubernetes para definir infraestructura como código

En Kubernetes todo se conoce como un objeto y estos objetos se definen en ficheros YAML.

Las definiciones se guardan y ejecutan en el cluster mediante el API Server.

La definición de objetos en Kubernetes también se conoce como infraestructura como código.

- **Pods**: Unidad más pequeña que se puede desplegar y gestionar en Kubernetes. Es un grupo de uno o más contenedores que comparte almacenamiento, red y especificaciones de ejecución. Son efímeros, es decir, se pueden crear y destruir fácilmente.
- **Deployments**: Describe el estado deseado de una implementación, ejecuta múltiples réplicas de la aplicación, reemplaza las que están defectuosas o las que no responden.
- **Services**: Definición de cómo exponer una aplicación que se ejecuta en un conjunto de pods como un servicio de red (por defecto se usa roud-robin para balanceo de carga).
- **Config Map**: Permite desacoplar la configuración para hacer las imágenes mas portables, almacenan variables de entorno, argumentos para la linea de comandos o configuración de volúmenes que pueden consumir los pods (no encriptación).
- **Labels**: Pares clave valor ("environment" : "QA") para organizar, seleccionar, consultar y monitorizar objetos de forma más eficiente, ideales para UI y CLIs.
- **Selectores**: Mecanismos para hacer consultas a las etiquetas. kubectl get pods -l environment in (production), tier in (frontend).

Para desplegar una aplicación en Kubernetes necesitamos como mínimo un pod, un deployment y un servicio.

### Instalación de Kubectl

Mini Kube es una herramienta que nos permite ejecutar un cluster de Kubernetes en una sola máquina, es ideal para pruebas y desarrollo.

Para instalar Mini Kube necesitamos instalar Kubectl, que es la herramienta de línea de comandos que nos permite interactuar con Kubernetes.

Una vez que tengamos Kubectl instalado podemos instalar Mini Kube con el siguiente comando:

```bash
brew install kubectl
```

Luego podemos iniciarlo con el siguiente comando:

```bash
minikube start
```

Con esto iniciamos un cluster de Kubernetes en nuestra máquina.

### Comandos para administrar minikube

- `minikube start`: Inicia un cluster de Kubernetes en nuestra máquina.
- `minikube stop`: Detiene el cluster de Kubernetes en nuestra máquina.
- `minikube status`: Muestra el estado del cluster de Kubernetes en nuestra máquina.
- `minikube dashboard --url`: Abre el dashboard de Kubernetes en el navegador.
- `minikube delete`: Elimina el cluster de Kubernetes en nuestra máquina.
- `minikube pause`: Pausa el cluster de Kubernetes en nuestra máquina.
- `minikube unpause`: Despausa el cluster de Kubernetes en nuestra máquina.
- `minikube addons list`: Lista los addons de Kubernetes en nuestra máquina.
- `minikube delete --all`: Elimina todos los clusters de Kubernetes en nuestra máquina.

### Crear un pod mediante Kubectl para desplegar una aplicación en Kubernetes

```bash
kubectl run kbillingapp --image=sotobotero/udemy-devops:0.0.1 --port=80 80
```

Con este comando creamos un pod en Kubernetes con la imagen `sotobotero/udemy-devops:0.0.1` y el puerto `8080`.

Si queremos ver los pods que se están ejecutando en el cluster podemos ejecutar el siguiente comando:

```bash
kubectl get pods
```

Y nos mostrará una lista de los pods que se están ejecutando en el cluster.

Para ver información mas detallada de un pod en particular podemos ejecutar el siguiente comando:

```bash
kubectl describe pod nombre_pod
```

Este comando nos mostrará información detallada de un pod en particular, como la dirección IP, el estado, los eventos, etc.

Para exponer el servicio en un puerto del host podemos ejecutar el siguiente comando:

```bash
kubectl expose pod nombre_pod --type=LodBalancer --port=8080 --target-port=80
```

Con este comando exponemos el servicio en el puerto `8080` del host.

Podemos comprobar que el servicio se ha expuesto correctamente con el siguiente comando:

```bash
kubectl get services
```

Para acceder a este servicio debemos pedir la url a minikube con el siguiente comando:

```bash
minikube service --url nombre_pod
```

Nos va a devolver una url que podemos pegar en el navegador para acceder al servicio.

### Comandos DevOps Jenkins

1. Consultar la version del apiserver

```bash	
kubectl api-versions
```

2. Codificar un parametro

```bash
echo -n 'qwerty' | base64
```

3. Descodificar un parametro

```bash
echo "cXdlcnR5" | base64 -d
```

4. Comandos necesario para apuntar el docker engine local hacia el registro de minikube

```bash
minikube docker-env
```

```bash
eval $(minikube -p minikube docker-env)
```

5. consultar la ip de minikube

```bash
minikube ip
```

### Encriptar variables de entorno sensibles

Para encriptar variables de entorno sensibles en Kubernetes podemos usar `Secrets`, que es un objeto de Kubernetes que nos permite almacenar información sensible, como contraseñas, claves de API, etc. Cuando trabajamos con K8 tenemos diferentes tipos de archivos de configuración, uno de ellos son los archivos de configuración de secretos.

Para esto podemos crear archivos con la extension YAML en donde definimos las variables de entorno sensibles, por ejemplo:

```yaml
# secret-dev.yaml

#object that store enviroments variables that could be have sensitive data like a password
apiVersion: v1
kind: Secret
metadata:
  name: postgres-secret
  labels:
    app: postgres
    #meant that we can use arbitrary key pair values
type: Opaque
data:
  POSTGRES_DB: cG9zdGdyZXM=
  POSTGRES_USER: cG9zdGdyZXM=
  POSTGRES_PASSWORD: cXdlcnR5
```

Este seria el archivo de configuración para la base de datos, en donde definimos las variables de entorno sensibles, codificadas en base64.

Necesitamos crear otro archivo para configurar el pod de DBMS, por ejemplo:

```yaml
# secret-pgadmin.yaml

#object that store enviroments variables that could be have sensitive data like a password
apiVersion: v1
kind: Secret
metadata:
  name: pgadmin-secret
  labels:
    app: postgres
    #meant that we can use arbitrary key pair values
type: Opaque
data:
  PGADMIN_DEFAULT_EMAIL: YWRtaW5AYWRtaW4uY29t
  PGADMIN_DEFAULT_PASSWORD: cXdlcnR5
  PGADMIN_PORT: ODA=
```

Este seria el archivo de configuración para el panel de administración de la base de datos, en donde definimos las variables de entorno sensibles, codificadas en base64.

### Almacenamiento persistente, volúmenes, claims y configmaps

En Kubernetes podemos usar volúmenes para almacenar datos de forma persistente, podemos configurar archivos de configuración para definir volúmenes, reclamos y mapas de configuración.

Un volumen es un directorio que contiene datos, un claim es una solicitud de almacenamiento persistente y un mapa de configuración es un objeto de Kubernetes que nos permite almacenar configuraciones en un archivo YAML.

Para definir un volumen en Kubernetes podemos usar el siguiente archivo de configuración:

```yaml
# persistence-volume.yaml

#persistence volumen (PV) is a piece of storage that have idependent lifecycle from pods 
#thees preserve data throug restartin, rescheduling and even deleting pods
#PersistenceVolumeCalin is a request for storage by the user that can be fulfilled by teh PV
kind: PersistentVolume
#version of ApiServer on control panel node (/api/v1) check using kubectl api-versions
apiVersion: v1
metadata:
  name: postgres-volume
  labels:
    #it is aplugin suport many luke amazon EBS azure disk etc.  local = local storage devices mounted on nodes.
    type: local
    app: postgres
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
    #many pods on shcheduled on differents nodes can read and write
  accessModes:
    - ReadWriteMany
    #path on cluster's node
  hostPath:
    path: "/mnt/data/"
```

Este seria el archivo de configuración para definir un volumen en Kubernetes, en donde definimos el nombre del volumen, la capacidad, el modo de acceso y la ruta del host.

Una ves definido este volume, necesitamos definir un archivo de configuración para el claim el cual hace una solicitud de almacenamiento persistente, por ejemplo:

```yaml
# persistence-volume-claim.yaml

#it is a reques of resource (persistence volume) from a pod by example, teh pod claim by a storage throug PVC
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: postgres-claim
  labels:
    app: postgres
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 2Gi
```

Es básicamente un archivo de configuración para definir un reclamo de almacenamiento persistente, en donde definimos el nombre del reclamo, el modo de acceso y los recursos solicitados.

Por último necesitamos definir un archivo de configuración para el mapa de configuración, este fichero contiene la inicialización de la base de datos, por ejemplo:

```yaml
# configmap-postgres-initdb.yaml

apiVersion: v1
kind: ConfigMap
metadata:
  name: postgres-init-script-configmap
data:
  initdb.sh: |-
   #!/bin/bash
   set -e
   psql -v ON_ERROR_STOP=1 --username "$POSTGRES_USER" --dbname "$POSTGRES_DB" <<-EOSQL
    CREATE USER billingapp WITH PASSWORD 'qwerty';
    CREATE DATABASE billingapp_db;
    GRANT ALL PRIVILEGES ON DATABASE billingapp_db TO billingapp;
   EOSQL
```

Este seria el archivo de configuración para definir un mapa de configuración en Kubernetes, en donde definimos el nombre del mapa de configuración y el script de inicialización de la base de datos.

### Definir el estado deseado de la aplicación: Deployments o manifesto

En Kubernetes podemos definir el estado deseado de la aplicación con un objeto llamado `Deployment`, este objeto nos permite definir el estado deseado de la aplicación, como el número de réplicas, la imagen, el puerto, etc.

Para definir un `Deployment` en Kubernetes podemos usar el siguiente archivo de configuración:

```yaml
# deployment-postgres.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres-deployment
  labels:
    app: postgres
spec:
#Pods number replicates
  replicas: 1
  #Define how the Deployment identify the pods that it could manage
  selector: 
    matchLabels:
     app: postgres
     #pod template specification
  template:
    metadata:
    #define teh labels for all pods
      labels:
        app: postgres       
    spec:
      containers:
        - name: postgres
          image: postgres:latest
          imagePullPolicy: IfNotPresent
          #open the port to allow send and receive traffic in teh container
          ports:
            - containerPort: 5432
            #read envars from secret file
          envFrom:
            - secretRef:
                name: postgres-secret
          volumeMounts:
          #This is the path in the container on which the mounting will take place.
            - mountPath: /var/lib/postgresql/data
              name: postgredb
            - mountPath: /docker-entrypoint-initdb.d
              name : init-script
      volumes:
        - name: postgredb
          persistentVolumeClaim:
            claimName: postgres-claim
        - name: init-script
          configMap:
             name: postgres-init-script-configmap
```

Este seria el archivo de configuración para definir un `Deployment` en Kubernetes, en donde definimos el nombre del `Deployment`, el número de réplicas, la imagen, el puerto, las variables de entorno, el volumen y el mapa de configuración.

Luego definimos el archivo de configuración `Deployment` para el panel de administración de la base de datos, por ejemplo:

```yaml
# deployment-pgadmin.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: pgadmin-deployment
spec:
  selector:
   matchLabels:
    app: pgadmin
  replicas: 1
  template:
    metadata:
      labels:
        app: pgadmin
    spec:
      containers:
        - name: pgadmin4
          image: dpage/pgadmin4        
          envFrom:
            - secretRef:
                name: pgadmin-secret
          ports:
            - containerPort: 80
              name: pgadminport
```

### Definición de servicios: Service

Podemos definir el objeto `Service` en Kubernetes para exponer la aplicación en un puerto del host. Para definir un `Service` en Kubernetes podemos usar el siguiente archivo de configuración:

```yaml
# service-postgres.yaml
kind: Service
apiVersion: v1
metadata:
  name: postgres-service
  labels:
    app: postgres
spec:  
  ports:
  - name: postgres
    port: 5432
    nodePort : 30432 
  #type: LoadBalancer
  type: NodePort
  selector:
   app: postgres
```

En donde definimos el nombre del servicio, el puerto, el tipo de servicio y el selector.

Luego definimos el archivo de configuración `Service` para el panel de administración de la base de datos, por ejemplo:

```yaml
# service-pgadmin.yaml
apiVersion: v1
kind: Service
metadata:
  name: pgadmin-service
  labels:
    app: pgadmin
spec:
  selector:
   app: pgadmin
  type: NodePort
  ports:
   - port: 80
     nodePort: 30200
```

### Crear los objetos en el cluster de Kubernetes

Una ves definidos todos estos objetos en archivos de configuración YAML, podemos crearlos en el cluster de Kubernetes con el siguiente comando:

```bash
kubectl apply -f archivo.yaml
```

Podemos hacerlo uno por uno o todos juntos, por ejemplo:

```bash
kubectl apply -f ./
```

Estando posicionados dentro de la carpeta que contiene todos los archivos de configuración con `./` indicamos que se ejecuten todos los archivos de configuración.

### Orquestar la aplicación

Una vez configurada la base de datos, los servicios y los volúmenes, nos queda agregar el frontend y el backend de la aplicación, para esto necesitamos definir los archivos de configuración correspondientes.

Por ejemplo, para el backend de la aplicación:

```yaml
# deployment-billingapp-back.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: billing-app-back-deployment
spec:
  selector:
   matchLabels:
    app: billing-app-back
  replicas: 3
  template:
    metadata:
      labels:
        app: billing-app-back
    spec:
      containers:
        - name: billing-app-back
          image: billingapp-back:0.0.4       
          ports:
            - containerPort: 7080
              name: billingappbport
```

Y para el frontend de la aplicación:

```yaml
# deployment-billingapp-front.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: billing-app-front-deployment
spec:
  selector:
   matchLabels:
    app: billing-app-front
  replicas: 2
  template:
    metadata:
      labels:
        app: billing-app-front
    spec:
      containers:
        - name: billing-app-front
          image: billingapp-front:0.0.4 
          ports:
            - containerPort: 80
              name: billingappfport
```

También necesitamos definir los servicios correspondientes, por ejemplo:

```yaml
# service-billingapp-back.yaml

kind: Service
apiVersion: v1
metadata:
  name: billing-app-back-service
  labels:
    app: billing-app-back
spec:   
  ports:
  - name: billing-app-back
    port: 7080
    nodePort : 30780 
  #type: LoadBalancer
  type: NodePort
  selector:
   app: billing-app-back
```

Y para el frontend:

```yaml
# service-billingapp-front.yaml

apiVersion: v1
kind: Service
metadata:
  name: billing-app-front-service
  labels:
    app: billing-app-front
spec:
  selector:
   app: billing-app-front
  type: NodePort 
  ports:
   - port: 80
     nodePort: 30100
```

Una ves definidos todos estos objetos en archivos de configuración YAML, podemos crearlos en el cluster de Kubernetes con el siguiente comando:

```bash
kubectl apply -f ./
```

## Gestión de repositorios y control de versiones con Git

Git es un sistema de control de versiones distribuido, opensource y se puede integrar con diferentes repositorios, puede usarse para controlar versiones de código, instalables, documentos, etc. Git se integra con diferentes repositorios centralizados como GitHub, GitLab, Bitbucket, etc.

Es común que cuando ser trabaja en equipo usando Git ocurran conflictos en los que se solapan cambios en el mismo archivo, para resolver este tipo de conflictos se suelen usar metodologías Git Flow o Git Trunk based para solventar este tipo de problemas.

### Git Flow vs Git Trunk based

Conceptos importantes:

- **Trunk**: Es la linea principal de desarrollo.
- **Branch**: Una nueva bifurcación del estado actual del código que crea una nueva ruta para evolucionar el código.
- **Fork**: Duplicar el repositorio y su historial de cambios.
- **Tag**: Etiquetas para identificar versiones del código en un momento dado (snapshot) es como moverse a una rama, pero sin poder modificar ni hacer commit, a menos que se cree una rama a partir de el tag.

#### Git Trunk based

Una única rama master de la cual parten los desarrolladores y crean ramas para sus características, cuando su rama está completa y ha sido probada se envía un MR a la rama principal (trunk/master).

1. Crea una rama de ciclo de vida corto partiendo del trunk/master.
2. Se realizan cambios en esta nueva rama y se agregan los commits. Se debe probar de manera exhaustiva localmente y en el servidor de integración continua.
3. Cuando esté listo para hacer merge, se debe actualizar la rama con los cambios de la rama principal para evita conflictos y agilizar el proceso.
4. Se debe hacer el Merge request de esta rama a la rama principal.

#### Git Flow

Es una metodología de flujo de trabajo aplicado a un repositorio de Git.

1. **Master**: Almacena ek historial de versiones oficiales, nunca recibe código directo.
2. **develop**: Funciona como rama de integración de las features, nunca recibe código directo.
3. **Features**: Parten de develop, son temporales, es aquí donde los desarrolladores agregan el código de nuevas características (feature/myFeature).
4. **Release**: Parten de develop, preparación de la release, se despliega en entorno de pruebas, se hacen ajustes y se integra en master y develop (release-x.y.z).
5. **Hotfix**: Parten de máster, para arreglar errores urgentes, se integran en master y dev y se marca la versión con un tag (hotfix-x.y.z).

Cuando usar Git Flow:

- Ideal para proyectos opensource.
- Cuando el número de desarrolladores junior es alto.
- Si el indice de rotación del equipo es alto.
- Cuando ya se cuenta con un producto establecido (en producción).
- Calendarios de releases fijo.

Cuando usar Git Trunk based:

- Es un practica requerida para la integración continua.
- Cuando se está iniciando un proyecto.
- Cuando se quiere iterar rápido
-  Cundo el equipo de desarrollo principalmente está integrado por seniors.
- Cuando se trabaja con enfoque TDD.

### Trunked based con Git

Para trabajar con Git Trunk based necesitamos tener una rama principal (trunk/master) y crear ramas para las características, por ejemplo:

```bash
git checkout -b feature/myFeature
```

Con este comando creamos una rama para una nueva característica. Luego podemos hacer cambios en esta rama y agregarlos al repositorio con los siguientes comandos:

```bash
git add .
git commit -m "Mensaje del commit"
```

Con estos comandos agregamos los cambios al repositorio y los guardamos en la rama. Luego podemos enviar la rama al repositorio con el siguiente comando:

```bash
git push origin feature/myFeature
```

Con este comando enviamos la rama al repositorio remoto. Luego podemos hacer un Merge Request para enviar la rama a la rama principal (trunk/master). Para hacer un Merge Request necesitamos ir al repositorio en GitHub, GitLab, Bitbucket, etc., y hacer clic en el botón de Merge Request.

Es importante recordar que antes de enviar la rama al repositorio remoto debemos actualizar la rama con los cambios de la rama principal para evitar conflictos y agilizar el proceso. Esto lo podemos hacer con el siguiente comando:

```bash
git pull origin trunk/master
```

Con este comando traemos a la rama los posibles cambios que pueden haber sido agregados a la rama principal mientras estábamos trabajando en nuestra rama.

### Git Flow con Git

Para trabajar con Git Flow necesitamos tener una rama principal (master) y una rama de desarrollo (develop), y crear ramas para las características, por ejemplo:

deberíamos comenzar moviéndonos a la rama develop:

```bash
git checkout develop
```

A partir de esta rama creamos una nueva para agregar lo cambios de nuestra feature:

```bash
git checkout -b feature/myFeature
```

Con este comando creamos una rama para una nueva característica. Luego podemos hacer cambios en esta rama y agregarlos al repositorio con los siguientes comandos:

```bash
git add .
git commit -m "Mensaje del commit"
```

Con estos comandos agregamos los cambios al repositorio y los guardamos en la rama. Luego podemos enviar la rama al repositorio con el siguiente comando:

```bash
git push origin feature/myFeature
```

Con este comando enviamos la rama al repositorio remoto. Luego podemos hacer un Merge Request para enviar la rama a la rama de desarrollo (develop). Para hacer un Merge Request necesitamos ir al repositorio en GitHub, GitLab, Bitbucket, etc., y hacer clic en el botón de Merge Request.

## Integración continua con Jenkins

### CI/CD Continuous Integration - Continuous Deployment

#### Integración continua

- Es una de las principales prácticas de DevOps y consiste en automatizar la gestión de los cambios del código de múltiples contribuidores en un único proyecto de software.
- Permite a los desarrolladores realizar merge frecuentemente en un repositorio central, luego permite que la compilación y pruebas automáticas sean ejecutadas.
- El sistema de control de versiones es el core de todo el proceso de integración continua y se puede complementar con pruebas de código automático, revision de sintaxis, pruebas de integración, pruebas de rendimiento, etc.

En este escenario de integración continua, tenemos 3 actores principales:

- **Desarrollador**: Es el encargado de escribir el código y subirlo al repositorio.
- **Repositorio**: Es el lugar donde se almacena el código fuente.
- **Servidor de Integración Continua**: Es el encargado de ejecutar las pruebas y desplegar la aplicación.

El desarrollador hace un push al repositorio, el servidor de integración continua detecta el cambio, descarga el código, ejecuta las pruebas y despliega la aplicación, puede ejecutar diferentes tipos de pruebas para asegurarse de que el código es correcto, ademas puede enviar notificaciones al desarrollador mediante correo electrónico, Slack, Discord, etc. Para alertar al desarrollador en caso de que algo salga mal. El servidor de integración continua compila el código, ejecuta las pruebas y despliega la aplicación en un entorno de pruebas.

#### Entrega continua

- Es una extensión del proceso de integración continua, dado que despliega todos los cambios de manera automática en el entorno de pruebas y/o producción.
- Se cuenta con un proceso de despliegue automatizado que se ejecuta después de la fase de construcción o deforma manual con frecuencia predeterminada.

#### Liberación continua

- Va un paso mas allá de la entrega continua en el nivel de automatización.
- Cuando la aplicación pasa todas las fases anteriores el software es desplegado en producción y entregado al cliente final, no hay intervención humana en el proceso, solo si las pruebas fallan se detendrá el proceso.

Una vez las nuevas características has sido probadas y validadas, se despliegan ya se en producción o en un entorno de pruebas, dependiendo de la configuración del pipeline.

#### Conceptos importantes

- Continuous Integration (CI)
  - Build
  - Test
  - Merge
- Continuous Delivery (CD)
  - Automatically release to repository
- Continuous Deployment
  - Automatically release to production

- **Pipeline**: Grupo lógico de actividades que de manera conjunta realizan tareas.
- **Jenkins**: Servidor de automatización de código abierto.
- **Slack**: Plataforma propietaria de comunicación empresarial (Característica mas relevante channel).
- **SonarQube**: Plataforma opensource para la inspección continua de la calidad del código, puede ejecutar revisiones automáticas.
- **Selenium**: Framework para probar aplicaciones web, permite escribir test funcionales de manera sencilla.

## Instalar y configurar Jenkins usando una imagen Docker extendida con Maven

Para descargar la imagen de Jenkins desde Docker Hub podemos ejecutar el siguiente comando:

```bash
docker pull jenkins/jenkins
```

Pero nosotros vamos a extender esta imagen con Maven, para esto necesitamos crear un archivo Dockerfile con el siguiente contenido:

```Dockerfile
FROM jenkins/jenkins
USER root
#Define variables
ENV MAVEN_VERSION 3.9.0

#Update Base OS and install additional tools
RUN apt-get update && apt-get install -y wget
RUN  wget --no-verbose https://downloads.apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz -P /tmp/
RUN tar xzf /tmp/apache-maven-$MAVEN_VERSION-bin.tar.gz -C /opt/ 
RUN ln -s  /opt/apache-maven-$MAVEN_VERSION /opt/maven 
RUN ln -s /opt/maven/bin/mvn /usr/local/bin 
RUN rm /tmp/apache-maven-$MAVEN_VERSION-bin.tar.gz 

#Set up permissions
RUN chown jenkins:jenkins /opt/maven;
ENV MAVEN_HOME=/opt/mvn
USER jenkins
```

Con este archivo creamos una imagen de Jenkins al cual le instalamos Maven, le instalamos Maven ya que vamos a usar Jenkins para compilar y desplegar aplicaciones Java.

Para construir la imagen con Maven necesitamos ejecutar el siguiente comando:

```bash
docker build -t jenkins-cicd --no-cache .
```

Con este comando construimos la imagen de Jenkins con Maven. Luego podemos ejecutar la imagen con el siguiente comando:

```bash
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins-cicd
```

Con esto creamo un contenedor de Jenkins con Maven. Luego podemos acceder a Jenkins en el navegador con la siguiente URL:

```bash
http://localhost:8080
```

Nos va a pedir una contraseña que podemos obtener con el siguiente comando:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Con esta contraseña podemos acceder a Jenkins en el navegador, nos va apedir instalar los plugins, podemos instalar los plugins recomendados o seleccionar los plugins que queremos instalar. Luego deberíamos crear un usuario y una contraseña para acceder a Jenkins.

### Diseñar un pipeline

Un pipeline es un conjunto de pasos que se ejecutan de manera secuencial, constan de varias etapas y cada etapa consta de varios pasos.

Por ejemplo, un pipeline sencillo:

- Pull.
- Build.
- Install.

Para crear esta pipeline primero debemos tener un proyecto con git conectado a un repositorio como GitHub por ejemplo

Luego debemos ingresar al Dashboar de Jenkins y selccionar la opcion `Create job`, luego en este caso seleccionamos un `freestyle project`, le ponemos un nombre, por ejemplo, `devops_test1` y seleccionamos la opción `OK`.


-Source Code Management
  - Luego en la sección de `Source Code Management` seleccionamos `Git`.
  - En la sección de `Repository URL` ingresamos la URL del repositorio.
  - Agregamos las credenciales del repositorio.
  - Seleccinamos la rama que queremos usar.
- Build Environment
  - En la sección de `Build steps` seleccionamos `Invoke top-level Maven targets`.
    - En la sección de `Goals` ingresamos `clean install`. Con esto limpiamos el proyecto y lo compilamos.
    - En advanced en la seccion `POM` ingresamos la ruta del archivo `pom.xml`, en este caso `billing/pom.xml`.

Con esto tenemos un pipeline sencillo que se encarga de instalar las dependencias y compilar el proyecto.

Ahora nos deberia aparecer en el dashboard de Jenkins el proyecto que acabamos de crear, podemos ingresar a el y seleccionar la opción `Build Now` para ejecutar el pipeline.

Podemos ingresar a la consola de Jenkins para ver los logs de la ejecución del pipeline en la seccion de `Console Output`.

Con esto se deberia ejecutar el pipeline y compilar el proyecto.

Para comprobar que el proyecto se instalo correctamente podemos ingresar a la consola de Jenkins y ejecutar el siguiente comando:

```bash
docker exec -it jenkins bin/bash
```

Con este comando ingresamos a la consola de Jenkins, luego podemos ejecutar el siguiente comando para ver los archivos del proyecto:

```bash
ls -la /var/jenkins_home/.m2/repository/ruta/proyecto/billing
```

Y con esto inspeccionamos la carpeta en la que jenkins nos dijo que se instalo el proyecto.

### Automatizar ejecución de pelines mediante eventos webHooks (ngrok, jenkins, git)

GitHub nos permite configurar WebHooks, esto es una forma de tener comunicación basada en eventos, de tal manera que cuando un evento sucede en el repositorio este evento puede ser notificado a diferentes interesados como por ejemplo nuestro servidor de Jenkins. Para que esto sea posible nuestro servidor Jenkins tiene que ser visible desde internet, para esto podemos usar una herramienta llamada ngrok.

Debemos descargar ngrok desde la página oficial y configurar lo con nuestro token personal de ngrok.

Ngrok es un proxy, como nuestro servidor de Jenkins está ejecutandose en local, no es visible desde internet, con ngrok podemos exponer el puerto de Jenkins a internet y ngrok va a manejar la comunicación entre internet y nuestro servidor de Jenkins.

Para exponer el puerto de Jenkins a internet con ngrok necesitamos ejecutar el siguiente comando:

```bash
./ngrok http 8080
```

Esto nos genera dos URLs, una para HTTP y otra para HTTPS, podemos usar la URL de HTTPs para configurar el WebHook en GitHub.

- En nuestro repositorio de GitHub vamos a la sección de `Settings`, luego a la sección de `WebHooks`, seleccionamos la opción de `Add WebHook`.
- En la sección de `Payload URL` ingresamos la URL de ngrok + `/github-webhook`.
- En la sección de `Content type` seleccionamos `application/json`.
- En la sección de `Which events would you like to trigger this webhook?` seleccionamos `Just the push event`.
. Luego seleccionamos la opción de `Add WebHook`.

Con esto cada vez que ocurra un evento de push en nuetro repositorio se enviara una notificación a Ngrok que a su ves la enviara a Jenkins.

### Crear un pipeline jenkins basado en el webhook

- En la consola de Jenkins vamos a la opción `administrar jenkins`.
- Seleccionamos la opción `configurar sistema`.
- Vamos a la seeción `github`.
- Seleccionamos la opción `add github server`.
- Le agregamos un nombre al `github server`
- En la seccion `credentials` seleccionamos `jenkins` se nos abrira una ventana en donde podemos configurar la credencial.
- En la sección `kind` seleccionamos `Secret text`.
- En la sección `Secret` ingresamos un token de github, debemos generar este token desde la cuenta de gh.
- Y presionamos el botón `Add`.

Ahora debemos crear un pipeline que use este webhook

- Marcamos la opción `GitHub proyect`.
- Ingresamos la URL de proyecto.
- En la sección `Configurar el origen del código` seleccionamos `Git`.
- Ingresamos la URL del repositorio, la que termina en `.git`.
- En la sección `Credentials` seleccionamos jenkins. Se nos habrira una ventana para configurar la credencial.
- En la seccón `Kind` seleccionamos `User with password` y ingresamo el usuario y la contraseña de la cuenta.
- En la sección `Branches to build` ingresamos el nombre de la rama que vamos a monitorear por ejemplo `origin/feature**` para monitorear todas la ramas que empiezen con el prefijo `feature`.
- En la seccion de `Disparadores de ejecuciones` seleccionamos `Github hook trigger`.
- En la sección `Ejecutar` seleccionamos `Ejecutar tareas 'maven' de nivel superior`.
- En la sección `Goles` ingresamos `clean install`
- En el apartado ``advanced``, en la sección `POM` ingresamos la ruta del fichero ``pom.xml``, por ejemplo `billing/pom.xml`.
- Presionamos `aplicar` y ``guardar``.

Con esto tenemos creado nuestro nuevo pipeline que hace uso del webhook de Github,se dispara cada vez que se hace un push en el repositorio y compila el proyecto.

### Integracipon continua

Un pipeline completo de integración continua, por ejemplo, deberia ejecutar todas las prubas unitarias, validar la calidad del código y si todo va bien hacer un merge en la rama principal y eliminar la rama de la característica.

Para esto debemos ingresar al pipeline que habiamos creado anteriormente y agregarle las etapas necesarias. 

- Ingresamos a la seccion `configurar`.
- En la seccion `Disparadores de ejecuciones` quitamos la opción `Github hook trigger`. Ya que esta etapa la vamos a agregar manualmente.
- En la seccion `Configurar el origen del código` seleccionamos la seccion `Additional Behaviours` y seleccionamos la opción `Custom user name/e-mail address`.
- En la sección `User name` ingresamos el nombre del usuario que va a hacer el commit. En este caso `jenkins`.
- En la sección `User e-mail address` ingresamos el correo del usuario que va a hacer el commit.
- En la sección `Ejecutar` seleccionamos `Añadir un nuevo paso` y seleccionamos `Ejecutar linea de comandos (shell)`.
- En la sección `Comando` ingresamos:
  - `git branch`
  - `git checkout main`
  - `git merge origin/feature/myFeature`
- En la seccion `Acciones para ejecutar después` seleccionamos `Añadir una opción` y seleccionamos `Git Publisher` nos mostrará una sección.
- En esa sección marcamos `Push Only If Build Succeeds`.
- En la sección `Branches` seleccionamso `Add Branch` y en la sección `Branch to push` ingresamos `main` y en la sección `Target remote name` ingresamos `origin`.
- Presionamos `aplicar` y `guardar`.

Con esto tenemos creado el pipeline de integración continua, que se encarga de clonar el repo, ejecuta las pruebas y si todo va bien hace un merge en la rama principal.

Jenkins nos permite crear pipelines mucho mas complejos que este, con multiples etapas y pasos, tiene un (repositorio de plugins)[https://plugins.jenkins.io/] que nos permite extender mucho su funcionalidad segun nuestras necesidades.

### Integrar Slack con Jenkins para enviar notificaciones y ver reportes de los pipelines

Slack es una plataforma de comunicación empresarial que nos permite integrar Jenkins para mediante notificaciones que nos llegan a un canal de Slack, nos informen del estado de los pipelines. Para esto en nuestro Slack debemos agregar una aplicación de Jenkins. Slack tiene una tienda de aplicaciones con diferentes aplicaciones que podemos integrar con Slack.

- Agregamos la aplicación de Jenkins a Slack.
- Seleccionamos el canal en el que queremos recibir las notificaciones. Podemos crear un nuevo canal llamado `jenkins`.
- En el panel de control de Jenkins vamos a la opción `administrar jenkins`.
- Seleccionamos la opción `administrar plugins`.
- Buscamos el plugin de Slack, `slack notification` y lo instalamos.
- Una vez instalado volvemos a la sección `administrar jenkins` y seleccionamos la opción `configurar sistema`.
- Vamos a la sección `Slack`.
- En la sección `Workspace` ingresamos el nombre de nuestro workspace de Slack.
- En la sección `Credential` seleccionamos `Add`.
- En la sección `Kind` seleccionamos `Secret text`.
- En la sección `Secret` ingresamos el token de Slack.
- Presionamos `Add`.
- Presionamos `aplicar` y `guardar`.

Ahora debemos habilitar las notificaciones de Slack en nuestro pipeline.

- Ingresamos a la sección `configurar` de nuestro pipeline.
- Vamos a la sección `Acciones para ejecutar después` y seleccionamos `Añadir una opción`.
- Seleccionamos `Slack Notifications`.
- Marcamos las opciones que queremos notificar como `Notify Build Start`, `Notify Build Failure`, `Notify Build Unstable`, `Notify Build Success`, `Notify Build Fixed`, `Notify Build Still Failing`. En este caso vamos a notificar en todos los casos.
- Seleccionamos nuevamente `Añadir una opción` y seleccionamos `Publicar los resultados de test JUnit`.
- En la sección `Ficheros XML con los informes de test` ingresamos la ruta del archivo de los informes de test, por ejemplo `billing/target/surefire-reports/*.xml`.
- Presionamos `aplicar` y `guardar`.

Con esto tenemos configurado nuestro pipeline para que nos envie notificaciones a Slack en caso de que ocurra un evento.

## Entrega continua y despliege continuo (CD) Sonarqube + Jenkins, Kubernetes

SonarQube es una plataforma opensource para la inspección continua de la calidad del código, nos permite ejecutar revisiones automáticas para verificar la calidad de este. SonarQube nos permite detectar errores, vulnerabilidades, bugs, duplicados, etc.

Para instalar SonarQube podemos hacerlo desde Docker Hub con el siguiente comando:

```bash
docker pull sonarqube
```

Luego podemos ejecutar la imagen con el siguiente comando:

```bash
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

Para que los contenedores de Jenkins con SonarQube se puedan comunicar deben estar en la misma red, para esto necesitamos crear una red en Docker con el siguiente comando:

```bash
docker network create jenkins_sonarqube
```

Luego debemos agregar los contenedores a la red con el siguiente comando:

```bash
docker network connect jenkins_sonarqube sonarqube
```

```bash
docker network connect jenkins_sonarqube jenkins
```

Para ver la interfaz de SonarQube debemos ingresar a la siguiente URL:

```bash
http://localhost:9000
```

El usuario y la contraseña por defecto son `admin`, `admin`.

Una vez dentro debemos ir a la sección de `Administration`, luego a la sección de `Security`, luego a la sección de `Users`.

- Generamos un token de acceso que posteriormente vamos a usar en Jenkins.
- Debemos ingresar a Jenkins e intalar el plugin de SonarQube `SonarQube Scanner`.
- Luego vamos a la sección de `administrar jenkins`, luego a la sección de `configurar sistema`.
- En la sección de `SonarQube servers` marcamos la opción `Enable injection of SonarQube server configuration as build environment variables`.
- En la sección de `Add SonarQube` ingresamos un nombre, por ejemplo `sonarqube`.
- En la sección de `Server URL` ingresamos la URL de SonarQube, como creamos una red con Docker la URL es `http://sonarqube:9000`.
- En la sección de `Server authentication token` ingresamos el token que generamos en SonarQube. Tambien podemos agregar este token en `Panel de control/ Crendenciales/ Sistema/ Crendenciales globales`.
- Presionamos `aplicar` y `guardar`.

Luego debemos ingresar a la sección `Global Tool Configuration` y agregar el `SonarQube Scanner`.

- Seleccionamos la opción `Add SonarQube Scanner`.
- Le ponemos un nombre, por ejemplo `sonarqube`.
- Marcamos la opción `Install automatically`.
- Presionamos `aplicar` y `guardar`.

## Agregar el escaneo de código con SonarQube al pipeline de Jenkins

Para esto debemos ingresar a la sección `configurar` de nuestro pipeline y agregar las etapas necesarias.

- Ingresaos a la sección `configurar` de nuestro pipeline.
- Vamos a la seccion `Ejecutar` y seleccionamos `Añadir un nuevo paso` y seleccionamos `Execute SonarQube Scanner`.
- En la sección `Analysis properties` ingresamos las propiedades de análisis, por ejemplo:
  - `sonar.projectKey=sonarqube`
  - `sonar.sources=billing/src/main/java`
  - `sonar.java.binaries=billing/target/classes`
- En la sección `Additional arguments` ingresamos `-X`.

Tambien debemos cambiar el orden de las etapas, para que el escaneo de código se ejecute primero, despues compilamos el proyecto y luego hacemos el merge.

Esta herramienta nos ayuda como desarrolladores a mejorar la calidad del código, analisa factores como Bugs, vulnerabilidades, duplicados, Code Smells, Coverage, Lines of Code, etc.

En la sección `issues` de SonarQube podemos ver los problemas que detecto en el código, SonarQube nos entrega un reporte detallado de los problemas que detecto en el código y nos da recomendaciones para solucionarlos.

### Crear imagen desde jenkins: Instalar y configurar el plugin de Docker

Podemos instalar el plugin de Docker en Jenkins para configurar un pipeline que nos permita crear una imagen de Docker y subirla a Docker Hub.

- Instalamos el plugin de Docker en Jenkins, `CloudBees Docker Build and Publish`.
- Debemos configurar el pipelien de Jenkins.
- Vamos a la seccion `Ejecitar` del pipeline y añadimos un nuevo paso, seleccionamos `Docke Build and Publish`.
- En la sección `Repository Name` ingresamos el nombre del repositorio de Docker Hub. `nombreRepo/billingapp-backend` por ejemplo.
- En la sección `Tag` ingresamos el tag de la imagen, por ejemplo `0.0.1`.
- En la sección `Docker Host URI` ingresamos la URL del host en donde está el Engine de Docker
  - Como tenemos Jenkins corriendo en un contenedor de Docker y el daemon de Docker corriendo en el host, debemos configurar un para que podamos compartir el daemon con el contenedor de Jenkins. Para esto debemos hacer un puente entre la red local y la red de Docker, para esto debemos ejecutar el siguiente comando:
  ```bash
  ip route show default | awk '/default/ {print $3}'
  ```
  Con este comando obtenemos la IP del host, luego debemos ejecutar el siguiente comando:
  ```bash
  ip a
  ```
  Con este comando obtenemos la IP de la interfaz de red, debemos buscar la red llama `docker0` para ver que segemento de red está usando Docker por ejemplo `172.17.0.1`

  - Con esa direccion ip armamos la URL de Docker, por ejemplo `tcp://172.17.0.1:2375` y la ingresamos en la sección `Docker Host URI`.
  - Tambien debemos hacer una configuración en el archivo de configuración de Docker `docker.service` para que Docker escuche en la red local, para esto debemos ejecutar el siguiente comando:
  ```bash
  sudo nano /lib/systemd/system/docker.service
  ```

  En el apartado `ExecStart` debemos agregar la siguiente linea:
  ```bash
  -H fd:// -H tcp://0.0.0.0:2375
  ```

  Debería quedar algo así:
  ```bash
  ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375
  ```
  - Luego debemos reiniciar el servicio de Docker con el siguiente comando:
  ```bash
  sudo systemctl daemon-reload
  sudo service restart docker
  ```
- En la sección `Registry Credentials` seleccionamos `Add` y agregamos las credenciales de Docker Hub.
- Presionamos `aplicar` y `guardar`.

En el proyecto del backend debemos ir archivo `aplication.properties` y agregar la siguiente linea:

```properties
server.port=7280
```

Ademas debemos agregar el Dockerfile en la raiz del proyecto con el siguiente contenido:

```Dockerfile
FROM openjdk:8-jdk-alpine
RUN addgroup -S devopsc && adduser -S javams -G devopsc
USER javams:devopsc
ENV JAVA_OPTS=""
ARG JAR_FILE
ADD ${JAR_FILE} app.jar
 # use a volume is mor efficient and speed that filesystem
VOLUME /tmp
EXPOSE 7280
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]
```

En el proyecto del frontend debemos agregar el Dockerfile en `src` con el siguiente contenido:

```Dockerfile
FROM nginx:alpine
 # use a volume is mor efficient and speed that filesystem
VOLUME /tmp
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY billingApp_prep /usr/share/nginx/html/billingApp_prep
COPY billingApp_prod /usr/share/nginx/html/billingApp_prod
#expose app and 80 for nginx app
EXPOSE 80 81
CMD ["nginx", "-g", "daemon off;"]
```

Ademas en el archivo `environment.prod.ts` debemos agregar el mismo puerto que en el backend:

```typescript
export const environment = {
  production: true,
  api_url: 'http://localhost:7280'
};
```

Lo mismo en el archivo `environment.ts`:

```typescript	
export const environment = {
  production: false,
  api_url: 'http://localhost:7280'
};
```

- En la sección `Ejecutar` del pipeline de Jenkins, en la parte de `Docker Build and Publish` debemos seleccionar la opción `advanced`.
- En la sección `Build context` ingresamos la ruta del proyecto, por ejemplo `billing/` para indicar donde está el Dockerfile.
- En la sección `Additional Build Arguments` ingresamos `--build-arg JAR_FILE=target/*.jar`.

### Deploy en kubernetes desde Jenkins

Para desplegar la aplicación en Kubernetes desde Jenkins necesitamos instalar el plugin de Kubernetes en Jenkins.

- Debemos conectarnos como root al contenedor de Jenkins con el siguiente comando:

```bash
docker exec -it --user=root jenkins bin/bash
```

- Una vez dentro del contenedor de Jenkins debemos instalar `kubectl`.
- Debemos conectar el contenedor de Jenkins a la misma red de minikube con el siguiente comando:

```bash
docker network connect minikube jenkins
```

- Luego hay que instalar el plugin de Kubernetes en Jenkins.

### Configurar el plugin de Kubernetes en Jenkins

- Debemos conseguir los datos necesarios de Kubernestes para configurar el plugin, estos datos son la `URL del servidor` y el `token`. Para esto debemos aplicar el siguiente archivo de configuración:

```yaml
# jenkins-account.yaml
#this file define a service account for kubernetesplugins on jenkins
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: jenkins
  namespace: default
---
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: jenkins
  namespace: default
rules:
- apiGroups: [""]
  resources: ["pods","services"]
  verbs: ["create","delete","get","list","patch","update","watch"]
- apiGroups: ["apps"]
  resources: ["deployments"]
  verbs: ["create","delete","get","list","patch","update","watch"]
- apiGroups: [""]
  resources: ["pods/exec"]
  verbs: ["create","delete","get","list","patch","update","watch"]
- apiGroups: [""]
  resources: ["pods/log"]
  verbs: ["get","list","watch"]
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get"]
- apiGroups: [""]
  resources: ["persistentvolumeclaims"]
  verbs: ["create","delete","get","list","patch","update","watch"]
 
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: jenkins
  namespace: default
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: jenkins
subjects:
- kind: ServiceAccount
  name: jenkins
---
# Allows jenkins to create persistent volumes
# This cluster role binding allows anyone in the "manager" group to read secrets in any namespace.
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: jenkins-crb
subjects:
- kind: ServiceAccount
  namespace: default
  name: jenkins
roleRef:
  kind: ClusterRole
  name: jenkinsclusterrole
  apiGroup: rbac.authorization.k8s.io
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  # "namespace" omitted since ClusterRoles are not namespaced
  name: jenkinsclusterrole
rules:
- apiGroups: [""]
  resources: ["persistentvolumes"]
  verbs: ["create","delete","get","list","patch","update","watch"]
```

- Lo aplicamos con el siguiente comando:

```bash
kubectl apply -f jenkins-account.yaml
```

- Luego debemos obtener la URL de donde esta el certificado del Cluster y  la URL del servidor, podemos obtener estos datos con el siguiente comando:

```bash
kubectl config view
```

- Tambien necesitamos el token de acceso de la cuenta que creamos en el archivo de configuración.

```bash
kubectl --namespace default get serviceaccount
```

- Verificamos que la cuenta de jenkins se creo correctamente.
- Vemos los detalles de la cuenta de jenkins con el siguiente comando:

```bash
kubectl --namespace default get serviceaccount jenkins -o yaml
```

- En donde nos interesa ver el name declarado, por ejemplo `jenkins-token-k2dqg`.
- Con esto podemos obtener el token de acceso con el siguiente comando:

```bash
kubectl describe secrets/jenkins-token-k2dqg
```

- Con esto obtenemos el token de acceso que necesitamos para configurar el plugin de Kubernetes en Jenkins.
- Agregamos este token en Jenkins en `Panel de control/ Crendenciales/ Sistema/ Crendenciales globales`, en donde agregamos el token y le ponemos una ID, por ejemplo `kubernetes-jenkins-server-account`.
- Ingresamos a la sección `administrar jenkins`, luego a la sección `configurar sistema`.
- Vamos a la sección `Cloud` y seleccionamos `Add a new cloud`.
- Seleccionamos `Kubernetes Cloud details`.
- En la sección `Kubernetes URL` ingresamos la URL del servidor de Kubernetes. La cual obtuvimos con el comando `kubectl config view`.
- En la sección `Kubernetes server certificate key` ingresamos el certificado del servidor de Kubernetes. La cual obtuvimos con el comando `kubectl config view`. por ejemplo `/home/user/.minikube/ca.crt` esta es la ruta del certificado, podemos ver el contenido del certificado con el comando `cat /home/user/.minikube/ca.crt`, es el contenido el que ingresamos en la sección `Kubernetes server certificate key`.
- Marcamos la casilla `Disable https certificate check`.
- En la sección `Credentials` seleccionamos la credencial de Kubernetes que creamos anteriormente.

Ahora debemos crear un pipeline que despliegue la aplicación en Kubernetes.

- Creamos un nuevo pipeline en Jenkins y seleccionamos la opción `Pipeline`.
- Seleccionamos la opción `GitHub project` y en la sección `Project url` ingresamos la URL del repositorio donde tenemos los archivos de configuración para el pipeline.
- En la seccion `Pipeline` en la sección `Definition` seleccionamos `Pipeline script from SCM`.
- En la sección `SCM` seleccionamos `Git`.
- En la sección `Repository URL` ingresamos la URL del repositorio, la que termina en `.git`.
- En la sección `Credentials` el usuario y la contraseña de la cuenta de GitHub.
- En la sección `Branch Specifier` ingresamos la rama, por defecto `main`.
- En la sección `Script Path` ingresamos la ruta del archivo de configuración del pipeline, por ejemplo `billing/Jenkinsfile`.

```groovy
pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        sh '''java -version
              mvn --version
              git --version'''
      }
    }

    stage('Deploy billing App') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://192.168.49.2:8443 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml '
          }

        }
      }

    }
  }
```

Este archivo de configuración del pipeline se encarga de clonar el repositorio, compilar el proyecto y desplegar la aplicación en Kubernetes.

- Presionamos `aplicar` y `guardar`.
- Podemos encadenar este pipeline con el anterior, para que una vez que se compile el proyecto se despliegue en Kubernetes. Para esto debemos ir a la sección `configurar` del pipeline anterior y en la sección `Acciones para ejecutar después` seleccionamos `Añadir una acción` y seleccionamos `Ejecutar otros proyectos`.
- En la sección `Proyecto a ejecutar` ingresamos el nombre del pipeline que acabamos de crear.

Con esto tenemos un pipeline que se encarga de clonar el repositorio, analizar el código con SonarQube, compilar el proyecto, crear una imagen de Docker y desplegar la aplicación en Kubernetes.