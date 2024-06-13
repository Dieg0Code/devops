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