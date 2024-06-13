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