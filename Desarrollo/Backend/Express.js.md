# Express.js
### Por que apredi express.js?
Al momento de hacer la revision de modulos para la creacion de servidores, express es el numero uno en todas las lista, despues viene el modulo Koa que fue creado por el mismo equipo, pero no logra alcanzar en popularidad a express.js .

### Datos de express

Minimalista o minimo: tiene un nucleo ligero con el cual se pueden hacer nuestras aplicaciones, esto no impide que pueda ser expandido con otras caracteristicas.
Template engines: Un template engine es una implementación de software que nos permite mezclar datos con una plantilla o template con el fin de generar un documento que será renderizado en el navegador.
Routing
Middlewares: Intercepcion de request o response para el mejor validacion de estos paquetes
Plugins

### Request y response
Request es la informacion del paqute de peticion que envia el cliente al servidor y response el el paquete de respuesta que el servidor arma.
Algunas propiedades de request son:
- req.body = Contiene los datos personalisados enviados por el cliente.
- req.params = Contiene las variables nombrados en la ruta.
    ```js
    app.get("/user/:id", function(req, res) {
        res.send("user " + req.params.id);
    });
    ```
- req.query = Esta propiedad guardar las variables adjuntadas en la ruta como una cadena de texto.
    ```js
    // GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
    req.query.order;
    ```
Las propiedades del response son:
- res.end() = Es un metodo heredado de nodejs, su funcion es indicar cuando la creacion del response termina y se tiene queenviar.
- res.json() = Recibe un objeto y lo transforma en json con JSON.strigify, despues lo envia dentro del response.
- res.send() = envia uns respueste HTTP, Buffer , texto plano,objeto, arreglo, etc.
- res.status() = Sirve para indicar el estado de la respuesta, segun https://developer.mozilla.org/es/docs/Web/HTTP/Status

### Acciones principales con express
Los primero, express tiene que ser inicializado (crear la aplicacion de express). En el ejeplo estamos indicando que se cree una nueva instancia de express y se relacione a la variable app, para luego desplegar ese servicio en un puerto que esta definido como una variable de entorno.
```ts
import express from "express";
const app = express()
app.listen(process.env.PORT,()=>{
    console.log('Listen on port http://'+os.networkInterfaces().eth0[0].address+':'+process.env.PORT)
})
```
Endpoint
Para crear un nuevo endpoint, usamos nuestra instacia de express y definimos su endpoint.

...

## Middleware
Hay 2 formas de añadir middleware en express.  
1. Añadiendo un middleware con `app.use()`, este se ejecutara para cualquier peticion en cualquier endpoint:
```ts
app.use((req:Request,res:Response,next:any)=>{
    console.log('consulta a '+ req.path); 
    next(); 
});
```
2. Añadiendo un middleware directo en el endpoint, este solo tendra efecto en el endpoint seleccionado:
```ts
router.get(
    '/...',
    validationHandler(object({ id: characterIdSchema }), 'params'), // middleware
    ...
)
```
### Manejo de errores con middlewares

El manejo de errores para procesos sincronos ya esta implementado en en express.Pero, los errores asincronos no se capturaran automaticamente. Tenemos q capturar el error y mandarlo por el next(err).
```ts
app.get("/", function(req, res, next) {
  fs.readFile("/file-does-not-exist", function(err, data) {
    if (err) {
      next(err); // Se debe pasar el error a Express.
    } else {
      res.send(data);
    }
  });
});
```

### JOI y BOOM
Paquetes q pertenecen originalmente al ecosistema de HAPI.
JOI -> Object Schema Validation
BOOM -> HTTP-frienly error objects

### BOOM
>Instalacion -> npm i @hapi/boom  
>Recordar: boom ya viene con sus types para typescript :v

### JOI
>Paquete que originalmente pertenecia al ecosistema de Hapi. Actualmente es idependiente de este.  
> ## Para que?  
>Permite la validacion de esquemas de datos  de una api. Es un paquete que valida los datos recibidos por una api esten en un formato aceptable para su uso dentro del backend.
> ## Importente
> _id de mongo puede ser validado con:
>  ```ts
>  joi.string().regex(/[0-9a-fA-F]{24}/);
>  ```

