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