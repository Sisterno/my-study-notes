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
    Elimina todos los contenedores q no esta actuamente activos.
- docker run ""
    --publish 8000:8000 : Permite la coexion desde afuera
- docker push ""
    Hace un push :v. Del repositorio completo o tag que tu especifiques. Importante; debes de hacer el build con el nombre apropiado.
- docker stop ""
    Para un contenedor. Que mas iba a hacer :v





## Proceso
 AWS Elastic Beanstack - es un servicio q permite el banceo de carga. Segun el numero de peticiones que se presenten se podra realizar un escalamiento horizontal.
