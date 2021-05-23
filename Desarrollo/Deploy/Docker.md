# Despligue de una app en docker con redis
## Por que?
Hitzii necesita despleguar su aplicacion,estamos usando una sistema de bases de datos intermedias REDIS. Este se despliega en docker. Mejor empesar a entender el despliegue de apps en contenedores.

## Teoria 

### Kubernetes

Cosas importantes a saber de un kubernetes:
- PODS : es tu espacio de trabajo, MV o sandbox que tiene una unica interfaz de red. Es la unidad minima con la que kubernetes trabaja para el escalamieento horizontal. Dentro tiene los contenedores con los servicios que tu definas. Todos los contenedores osn procesos hermanos.
- Docker: Docker es una aplicacion q permite la gestion de haraware para contenedores. Docker controla los contenedores a nivel de hardware. 
- Contenedor

### Docker
Docker realiza el manejo de imagenes. Nos permite crear, duplicar o eliminar imagenes que en un futuro pueden ir en un contenedor.

#### Crear una imagen
Para crear una imagen es necesario 


#### Comandos
- **docker ps**
    Lista los contenedores que estan activos actualmente.
    Con -a, lista todos los contenedores.
- **docker build**
    Segun el archivo ***Dockerfile***
    -t o --tag : Le pones nombre a tu imagen. Lo importante es q si quieres hacer un push en un futuro este tendra q ir a un repositorio. para esto el tag debe de ser "nombre del repo:tag".
- **docker inspect ""**
    Muestra toda la info del docker.
- **docker rm ""**
    Elimina un contenedor
- **docker container prune**
    Elimina todos los contenedores q no esta actualmente activos.
- docker run ""
    --publish 8000:8000 : Permite la conexión desde afuera
    --rm : Cuando el contenedor se detenga, elimíname este contenedor
- docker push ""
    Hace un push :v. Del repositorio completo o tag que tu especifiques. Importante; debes de hacer el build con el nombre apropiado.
- docker stop ""
    Para un contenedor. Que mas iba a hacer :v

#### Comandos para otros casos

`docker run -d --name db **mongo`

​	Creación de un contenedor con mongodb

`docker exec -it db bash`

​	Permite tener accesos a la consola bash del contenedor y manejarlo.

​	

---

## Volúmenes

Los volúmenes nos permite sincronizar carpetas y subcarpetas de nuestro contenedor con un directorio de nuestra maquina.

### Bind mounts

En este ejemplo usamos un contenedor con mongo donde todos los datos de las db se sincronicen con una carpeta. Si en un futuro eliminamos el contenedor; podemos volver a crear y montar la misma carpeta para recuperar los datos  que teníamos en el anterior contenedor.

```
docker run -d --name db -v /mnt/d/docker/mongodata:/data/db mongo  
```

El problema de usar este método de montar carpetas es que cualquier usuario de nuestra maquina o cluster puede acceder a esa misma carpeta y alterar los datos. Alterar estos archivos puede ocasionarnos problemas con nuestro contenedor.



### Volume

LA creación de un volumen nos permite tener una copia de archivos de una ruta de nuestro contenedor guarda en nuestro clúster. Con los volúmenes tenemos la ventaja de que Docker los administra y nosotros no tendremos que preocuparnos por  su administración ya que solo el tiene acceso a esos datos. Aunque también hay métodos complejos para entrar a estos datos.

`docker volume ls` -> Lista los volúmenes del clúster.

`docker volume create dbdata` -> Creación de un volumen con el nombre dbdata 

`docker run -d --name db --mount src=dbdata,dst=/data/db mongo` -> Creo la imagen de mongo montando nuestro volumen dbdata en el destino (dentro de nuestro contenedor) /data/db



### Insertar y extraer archivos de un contenedor

`docker cp "src" "dst"`

​	Permite copiar archivos y carpetas de dentro de un contenedor a nuestro sistema y viceversa.

​	Ejem

​	`docker cp dbcontainer:/test/mi.txt ~/docker/`

​		Copia el archivo `mi.txt` del contenedor `dbcontainer` a nuestra carpeta `~/docker` 

​	`docker cp ~/docker/ dbcontainer:/test/`

​		Copia el contenido de `~/docker`  a la carpeta `/test/` del contenedor `dbcontainer`

---

## Imágenes

Es la unidad mínima para crear un contenedor. Las imágenes contienen los archivos  necesarios para el despliegue de nuestro contenedor. La imagen contiene paquetes, archivos de sistema operativo, ejecutadores, u otros archivos.

Docker hub este el repositorio principal de docker. Aqui podemos encontrar las imagenes pordefecto de sistema operativos, bases de datos, apps populares, herramientas para el apoyo de applicaciones en docker.

`docker pull ""` -> Trae una imagen del repositorio de docker hub, se puede especificar de que repositorio traer una imagen.

### Dockerfile

Nos permite crear nuevos imágenes con las características que nosotros queramos. Pro ejemplo:

```dockerfile
FROM node:14.16.0
# ENV NODE_ENV=production
EXPOSE 3031
# WORKDIR ./

COPY ["package.json", "package-lock.json*", "./"]

# RUN npm install --production
RUN npm install


COPY . .
RUN npm run build

CMD [ "node", "./build/app.js" ]

# CMD [ "node", "server.js" ]
# CMD [ " npm run dev" ]
```

`docker build -t <nombre de imagen>:<tags> <Dockerfile context>`

​	Buildea la imagen

`docker login -u <username> -p <password>`

​	Loguearse con tu cuenta de docker hub

`docker tag <name>:<tag> <name del repositorio>/<name>:<tag>`

​	Retagear una imagen, para cuando quieres especificar a que repositorio lo quieras pushear :v

`docker push <name completo>`

​	Hace un push a repositorio del tag de la imagen.

### Sistema de capas

Cada comando del dockerfile se considera una capa al momento de realizar el build de nuestra imagen.

`docker history <name image>`

​	Muestra las capas de una imagen.

Para tener una mejor vision de nuestras capas, podemos usar la app de `Dive` . Dive es un app externa desarrollada por Wagoodman su repositorio es https://github.com/wagoodman/dive 

`docker <docker image>` 

​	Muestra información del trabajo de cada capa, similar en proceso a `docker history <name image>` pero con mucha mas información.

#### Capas de dockerfile

Copiar nuestro archivo desde el diretorio donde se realiza al build. Copianmos 

```dockerfile
copy [x.js,y.js,..., /mnt/home/]
```



### Info extra

Con `docker commit <container>` podemos crear una imagen desde un contenedor con todos los cambios que se realizo al contenedor durante su tiempo de vida hasta el commit.

---

## Docker compose



### docker-compose.override.yml

La creación de un archivo override permite el trabajo cooperativo en nuestros proyectos. Permite realizar cambios en docker-compose si tener que alterar el archivo principal. Docker trata de realizar un merge para poder realizar el proceso de build con ambos archivos.





---

## Herramientas avanzadas de docker

### Limpieza y mantenimiento de docker en nuestra maquina

`docker container prune` -> Borrar todos los contenedores inactivos

`docker rm -f $(docker ps -aq)` -> Borrar a la fuerza todos nuestros contenedores sin importar si esta activos o inactivos.

`docker system prune` -> Borrar todo lo que no se este utilizando que este relacionado con docker (contenedores, volúmenes, imágenes, etc)

`docker run -d --name app --memory 1g platziapp` -> solo utilizara 1gb de nuestra memoria ram

`docker stats` ->  ver el consumo de hardware de nuestro contenedores y docker en general.

`docker inspect <contenedor>` -> muestra información de nuestros contenedores, en este caso nos interesaría ver que en caso de q nuestro contenedor tenga problemas para correr, aquí se puede ver que error esta pasando.

### Deteniendo contenedores

Cuando docker debe detener un contenedor, este manda un `SYGTERM` y en caso de que lo queramos matar a la fuerza se manda un `SYGKILL` 

`docker ps -l` -> muestra es estado del ultimo contenedor, este o no funcionando. Nos ayuda mas en debugin para saber por que murió nuestro ultimo contenedor. Código de status >128, error , algo malo pudo pasar.

`docker exec <container> ps -ef` -> Muestra los procesos dentro de nuestro contenedor

#### Formato shell y formato exec

En este caso nos referimos a formato al la forma de escribir nuestra capa de ejecucion del proceso principal en nuestro dockerfile.

El formato shell hace referencia a como ejecutaríamos el proceso en una terminal. La principan diferencia es que al usar el formato shell nuestro proceso principal no se genera como tal, sino se genera como un proceso hijo del proceso principal. El formato exec es el mas optimo para no tener problemas con detener procesos.

```dockerfile
CMD "node server.js" 			#Esta seria el formato shell
CMD ["node","|server.js"]	  #Esta seria el formato exec
```

## Contenedores ejecutables

En caso de querer pasar un parámetro desde la ejecución del docker run, podemos alterar el dockerfile para este fin. Un ejemplo seria:

```dockerfile
...
ENTRYPOINT [ "/bin/ping", "-c", "3"]
CMD ["localhost"]
```

Este docker file indica que siempre se va a empesar el proceso principal con el comando definido en `ENTRYPOINT` , pero los parametros definidos en CMD pueden cambiar al momento de ejecutar nuestro comando de `docker run` con:

```bash
# docker run --name pinger ping <parametro>
 docker run --name pinger ping google.com  
```

 El parámetro en vez de ser 'localhost' del CMD de dockerfile, va a ser 'google.com'

### Context de build

El conexto de build hacer referencia al acceso de nuestra computadora que docker tiene acceso al momento de realizar el build de una imagen. en caso de que queramos hacer es ignorar archivos para nuestro build se puede usar `.dockerignore`

#### .dockerignore

Permite definir que archivos no debe de considerar para el contexto de build.

### Multi-stage build

Nos referimos a multi-stage cuando queremos que en un proyecto se realiza un proceso antes de definir la imagen final para un contenedor. En el siguiente ejemplo tenemos un caso de uso en el cual queremos realizar un proceso donde se corra los test de nuestra aplicación y una vez que se satisfagan estos test, queremos construir la imagen pero que esta imagen no contenga los archivos que se necesitaban para los test, sino solo los necesarios para su estado en produccion. 

Para esto primero hacemos un stage donde se instalan todo lo necesario para realizar los test de validación de nuestro proyecto. Una vez que se pasen los test, definimos otro stage donde solo se pedirá las dependencias de producción y se copiaran los archivos del stage anterior, así nuestra imagen estará mas limpia y nos aseguraremos de que esta perfectamente aceptable con los test que el equipo de desarrollo definió.

```dockerfile
FROM node:12 as builder
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install --only=production
COPY [".", "/usr/src/"]
RUN npm install --only=development
RUN npm run test

# Productive image
FROM node:12

COPY ["package.json", "package-lock.json", "/usr/src/"]

WORKDIR /usr/src

RUN npm install --only=production

COPY --from=builder ["/usr/src/index.js", "/usr/src/"]

EXPOSE 3000

CMD ["node", "index.js"]
```

### Docker in docker

Docker deamon expone un interfaz que nos permite realizar la conexion con ese sockert. Asi que si queremos por alguna razón crear un contenedor que tenga acceso al docker de nuestro cluster, se puede hacer montando el documento de docker daemon en un contenedor y conectándolo.

```bash
docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:19.03.12
```

Un uso de esta capacidad es que si quermos usar una aplicacion que no queremos instalar en nuestra maquina principal, la podemos ejecutar en un contenedor que mediante el docker.sock tiene acceso al docker de nustra maquina principal. 

```bash
docker run --rm -it -v /var/run/docker.sock:/var/run/docker.sock -v $(wich docker):/bin/docker wagoodman/dive:latest prodapp
```

Importante

:v tener mucho cuidado con esto que podemos hacer que maquina q no conocemos tengan acceso a nuestra maquina. Recuerda las cosas que hiciste en la u cuando desactivamos el firewall  de una maquina aprendiendo a tener acceso al bash con un jpg ejecutable. :v

## Proceso
 AWS Elastic Beanstack - es un servicio q permite el banceo de carga. Segun el numero de peticiones que se presenten se podrá realizar un escalamiento horizontal.