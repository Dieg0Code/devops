# Commandos básico y utiles para el curso

## Índice

1. [**Network tools**](#network-tools)
    - [Linux](#linux)
    - [Windows Power shell](#windows-power-shell)
2. [**Docker**](#docker)
    - [Trabajando con imágenes del container registry](#trabajando-con-imágenes-del-container-registry)
    - [Construyendo Imágenes](#construyendo-imágenes)
    - [Comandos Avanzados para Imágenes](#comandos-avanzados-para-imágenes)
    - [Comandos para la Gestión Básica de Contenedores](#comandos-para-la-gestión-básica-de-contenedores)
    - [Trabajando con Redes y Volúmenes](#trabajando-con-redes-y-volúmenes)
    - [Interactuando con Contenedores](#interactuando-con-contenedores)
    - [Docker Compose](#docker-compose)
    - [Administración de Redes y Volúmenes](#administración-de-redes-y-volúmenes)
    - [Comandos para Información y Estadísticas](#comandos-para-información-y-estadísticas)
    - [Comandos para Seguridad y Control de Acceso](#comandos-para-seguridad-y-control-de-acceso)
    - [Comandos para Configuraciones Avanzadas](#comandos-para-configuraciones-avanzadas)

## Network tools

### Linux 
1. Install this tool to management network options
```shell
sudo apt install net-tools 
sudo apt-get install telnet
```
* Check ports listening
```shell
netstat -n --all --tcp
```
* Find specific port 
```shell
sudo lsof -i -P -n | grep 9000
```
* Testing socket whit telnet, teh format telnet ipaddress port
```shell
telnet localhost 5433
```

 ### Windows Power shell 

* Check ports listening
```powershell
Get-NetTCPConnection
```
* Obtener todas las conexiones TCP
```powershell
$connections = Get-NetTCPConnection
```
* Filtrar conexiones en estado 'Listen' o 'Established'*
```powershell
$filteredConnections = $connections | Where-Object {($_.State -eq 'Listen') -or ($_.State -eq 'Established')}
```
* Obtener información detallada de cada conexión*
```powershell
$connectionDetails = $filteredConnections | ForEach-Object {
    $localPort = $_.LocalPort
    $remotePort = $_.RemotePort
    $state = $_.State
    $processId = $_.OwningProcess
    $process = Get-Process -Id $processId
    $processName = $process.ProcessName

    [PSCustomObject]@{
        LocalPort = $localPort
        RemotePort = $remotePort
        State = $state
        Application = $processName
    }
}
```
* Mostrar la información en la consola
```powershell
$connectionDetails
```
* Find specific port 
```powershell
Get-NetTCPConnection | Where-Object {$_.LocalPort -eq 9000}
```
* Testing socket whit telnet, teh format telnet ipaddress port
```powershell
Test-NetConnection -ComputerName localhost -Port 5433
```

## **Docker**
### Trabajando con imágenes del container registry

- **Descargar una imagen desde Docker Hub:**
```shell 
#docker pull nombre_de_la_imagen
docker run -d -p 80:80 docker/getting-started
```
- **Listar imágenes locales:**
```shell 
docker image ls
```
- **Crear y ejecutar un contenedor a partir de una imagen:**
```shell 
#docker run [opciones] nombre_del_contenedor nombre_de_la_imagen
docker run -p 80:80 -p 7080:7080 --name containerBilling sotobotero/billingapp
```
- **crear un contenedor de postgres y una base de datos en el mismo comando:**
```shell
docker run --ulimit memlock=-1:-1 -d --name postgres -e POSTGRES_USER=sa -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=product_db -p 5432:5432 postgres:13.3
```
- **Listar contenedores en ejecución:**
```shell 
docker ps
```
- **Listar todos los contenedores (incluso los detenidos):**
```shell 
docker ps -a
```
- **Detener todos los contenedores:**
```shell 
docker stop $(docker ps -q)
```
- **Iniciar todos los contenedores:**
```shell 
docker start $(docker ps -a -q)
```
- **Eliminar todos los contenedores:**
```shell 
docker rm $(docker ps -a -q)
```
### Construyendo Imágenes

- **Construir una imagen desde un Dockerfile:**
 ```shell
 #docker build -t nombre_de_la_imagen [opciones y parametros] .
 docker build -t billingapp --no-cache --build-arg JAR_FILE=target/*.jar .
```
- **Construir una imagen con un contexto específico:**
 ```shell
  docker build -t nombre_de_la_imagen -f ruta/Dockerfile .
```
### Comandos Avanzados para Imágenes

- **Etiquetar una imagen:**
 ```shell
 docker tag nombre_de_la_imagen nueva_etiqueta
```
- **Loguears en un registry:**
 ```shell
docker login # te pedirá usuario y contraseña
 ```
- **Subir una imagen a Docker Hub:**
 ```shell
  docker push nombre_de_la_imagen
```
- **Descargar una imagen con una etiqueta específica:**
 ```shell
  docker pull nombre_de_la_imagen:etiqueta
```
- **Desloguearse de un registry:**
 ```shell
docker logout
 ```
### Comandos para la Gestión Básica de Contenedores

- **Detener un contenedor en ejecución:**
```shell 
docker stop nombre_del_contenedor
```

- **Iniciar un contenedor detenido:**
```shell 
docker start nombre_del_contenedor
```
- **Eliminar un contenedor:**
```shell 
docker rm nombre_del_contenedor
```
- **Eliminar una imagen local:**
```shell
docker image rm nombre_de_la_imagen
```
### Trabajando con Redes y Volúmenes

- **Crear una red personalizada:**
 ```shell 
 docker network create nombre_de_la_red
```
- **Listar redes:**
 ```shell
 docker network ls
```
- **Crear un volumen:**
 ```shell
 docker volume create nombre_del_volumen
```
- **Listar volúmenes:**
 ```shell
 docker volume ls
```
### Interactuando con Contenedores

- **Ejecutar un comando en un contenedor en ejecución:**
 ```shell
 #docker exec -it nombre_del_contenedor comando
docker exec -it localbillingApp sh
```
- **Copiar archivos entre el host y un contenedor:**
 ```shell
  docker cp archivo.txt nombre_del_contenedor:/ruta/destino
  ```
### Docker Compose

- **Iniciar contenedores definidos en un archivo `docker-compose.yml`:**
 ```shell
  docker-compose up
```
- **Escalar servicios en Docker Compose:**
 ```shell
  docker-compose scale servicio=num_instancias
```
- **Detener y eliminar contenedores definidos en Docker Compose:**
 ```shell
  docker-compose down
```
- **Ver logs de servicios en Docker Compose:**
 ```shell
  docker-compose logs servicio
```
### Administración de Redes y Volúmenes

- **Eliminar una red:**
 ```shell
  docker network rm nombre_de_la_red
```
- **Eliminar un volumen:**
 ```shell
  docker volume rm nombre_del_volumen
```
- **Inspeccionar una red:**
 ```shell
 docker network inspect nombre_de_la_red
```
### Comandos para Información y Estadísticas

- **Ver detalles de un contenedor:**
 ```shell
  docker inspect nombre_del_contenedor
```
- **Obtener estadísticas de uso de recursos de un contenedor:**
 ```shell
  docker stats nombre_del_contenedor
```
- **Obtener estadísticas de uso de recursos de todos los contenedores:**
 ```shell
  docker stats
```
### Comandos para Seguridad y Control de Acceso

- **Crear un perfil de control de acceso (se requiere Docker EE):**
 ```shell
  docker trust key generate nombre_de_perfil
```
- **Especificar qué usuarios o equipos pueden o no usar Docker:**
 ```shell
  docker trust key load --alias nombre_de_perfil.pem --pem --root /etc/docker/pki/tls/private
```

- **Inhabilitar Docker para usuarios no autorizados (se requiere Docker EE):**
 ```shell
  docker trust signer remove nombre_de_perfil
```
### Comandos para Configuraciones Avanzadas

- **Crear un contenedor con un archivo de configuración personalizada:**
 ```shell
  docker run -v ruta/local:/ruta/contenedor -e variable_de_entorno=valor nombre_de_la_imagen
```
- **Especificar recursos de sistema para un contenedor (CPU, memoria, etc.):**
 ```shell
 docker run --cpu-shares=512 -m 256m nombre_de_la_imagen
```
- **Elimina todos los contenedores detenidos e imagenes que no esten en uso**
 ```shell
docker system prune --all
 ```
 - **Elimina todos los volumenes que no esten en uso**
 ```shell
docker volume prune
 ```
 - **Elimina todas las redes que no esten en uso, menos las por defecto (bridge, none,host)**
 ```shell
docker network prune ```
 ```
 ## docker Swarm
   - **Ver informacion de la instalación de docker:**
 ```shell
   docker info
```
 - **Inicializar Docker Swarm:**
 ```shell
   docker swarm init
```
 - **Unirse a un clúster Swarm:**
 ```shell
   docker swarm join --token <token>
```
 - **Desplegar un servicio:**
 ```shell
   docker service create --name <nombre_servicio> <imagen>
```
 - **Listar servicios en ejecución:**
 ```shell
   docker service ls
```
 - **Ver detalles de un servicio:**
 ```shell
   docker service inspect <nombre_servicio>
```
 - **Escalar un servicio:**
 ```shell
   docker service scale <nombre_servicio>=<número_replicas>
```
 - **Actualizar un servicio:**
 ```shell
   docker service update --image <nueva_imagen> <nombre_servicio>
```
 - **Eliminar un servicio:**
 ```shell
   docker service rm <nombre_servicio>
```
 - **Ver nodos en el clúster:**
 ```shell
   docker node ls
```
 - **Ver información detallada de un nodo:**
 ```shell
    docker node inspect <ID_nodo>
```
 - **Quitar un nodo del clúster:**
 ```shell
    docker node rm <ID_nodo>
```
 - **Pausar un servicio:**
 ```shell
    docker service pause <nombre_servicio>
```
 - **Reanudar un servicio:**
 ```shell
    docker service resume <nombre_servicio>
```
 - **Ver logs de un servicio:**
 ```shell
    docker service logs <nombre_servicio>
```
 - **Ver eventos del clúster:**
 ```shell
    docker swarm events
```
 - **Obtener token de manager:**
 ```shell
    docker swarm join-token manager
```
 - **Obtener token de worker:**
 ```shell
    docker swarm join-token worker
```
 - **Promover un nodo a manager:**
 ```shell
    docker node promote <ID_nodo>
```
 - **Despromover un nodo a worker:**
 ```shell
    docker node demote <ID_nodo>
```
 - **Actualizar la clave de autenticación del manager:**
 ```shell
    docker swarm update --autolock=true
```

Descargar imagen sonar

```shell
docker pull sonarqube
```

Crear contenedor de sonar

```shell
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

crear red virtual

```shell
docker network create jenkins_sonarqube
```

verificar redes

```shell
docker network ls
```

conectar los contenedores a la red virtual

```shell
docker network connect jenkins_sonarqube sonarqube
docker network connect jenkins_sonarqube reverent_robinson (cambiar por el nombre que cada uno tenga para el contendor jenkins)
```

Ver los detalles de un contenedor

```shell
docker container inspect sonarqube 
```

parametros de la configuración del paso referente a sonar

```shell
scan
-X
```

Propiedades usadas en la configuracion del pipeline para añadir el paso de sponarqube

```
sonar.projectKey=sonarqube
sonar.sources=billing/src/main/java
sonar.java.binaries=billing/target/classes
```

## Configurar el agente de Docker para construir la imagen en el pipeline

### Plugin que debe ser instalado
- **CloudBees Docker Build and Publish**

### Nombre de imagen
- **cuentadockerhub/billingapp-backend**

### URL del agente
- **tcp://172.17.0.1:2375**

### Contexto para la imagen del backend
- **billing/**

### Argumentos adicionales
- `--build-arg JAR_FILE=target/*.jar`

### Ruta del fichero que se debe editar en el host para exponer el API del daemon de Docker
- **/lib/systemd/system/docker.service**

**Usar `nano` o `vi` con `sudo` para poder guardar.**

### Ajustar el contenido de la línea para que quede como esta:
- `ExecStart=/usr/bin/dockerd -H fd:// -H=tcp://0.0.0.0:2375`

### Reiniciar servicios
```sh
sudo systemctl daemon-reload
sudo service docker restart
```

### Verificar y/o reiniciar contenedores de Docker
- `docker ps` -> Ver contenedores activos
- `docker ps -a` -> Ver todos

### Comprobar que el API es accesible mediante el protocolo HTTP con el siguiente comando o en un navegador
```sh
curl http://localhost:2375/images/json
```

### Hacer puente entre el contenedor de Jenkins y el host local para acceder al Docker daemon mediante TCP
```sh
ip route show default | awk '/default/ {print $3}'
```
Después:
```sh
ip a
```
Buscar la red de Docker 01 y usarla en lugar de localhost. En la configuración del plugin en el pipeline debería ser `172.17.0.1` o similar.

---

## Configurar la integración con Kubernetes

### Conectarse como root en Jenkins e instalar el `kubectl`
```sh
docker exec -it --user=root jenkins /bin/bash
```

### Conectar Jenkins a la red de Minikube
```sh
docker network ls
docker network connect minikube jenkins
```

### Plugin que debe ser instalado
- **Kubernetes plugin**

### Ver la configuración de Minikube
```sh
kubectl config view
```

### Consultar los service account
```sh
kubectl --namespace default get serviceaccount
```

### Ver el detalle del service account
```sh
kubectl --namespace default get serviceaccount jenkins -o yaml
```

### Obtener el token del service account
```sh
kubectl describe secrets/jenkins-token-rk2mg
```
1- Namespaces: Clusters virtuales en un mismo cluster fisico (separacion logic ade clusters)

  ```bash
  https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
  ```

2-verificar namespaces

```bash
kubectl get namespace
```

3- Crear el namespace si no existe
```bash
kubectl create namespace monitoring
```

4-Crear role de monitorizacion

   - Referencia Authoriation
   
   ```bash
   https://kubernetes.io/docs/reference/access-authn-authz/rbac/
   kubectl apply -f moniring-role.yaml
   ```
5- Crear fichero de configuracion para externalizar la configuracion de prometheus(independiente del ciclo de vida del contenedor)

```bash
kubectl apply -f configmap-prometheus.yaml
```
6- Crear el contenedor y el servicio de prometheus (el contenedor)

```bash
kubectl apply -f deployment-prometheus.yaml
```

7- verificar los pods del namespace  monitoring
```bash
kubectl get all --namespace=monitoring
```