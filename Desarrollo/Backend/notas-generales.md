# Notas sobre desarrollo de backend

### Informacion del sistema operativo

Para obtener informacion del sistema operativo se puede utilizar el modulo 'os':

```javascript
const os = require('os');

console.log('cpu info',os.cpus())
console.log('ip address', os.networkInterfaces())
console.log('free memory', os.freemem())
console.log('Type',os.type())
console.log('SO release',os.release())
console.log('user data',os.userInfo())
```
### Manejo de directorios y archivos
Tambien se puede ralizar el manje de directorios y archivos con el modulo 'fs':

```javascript
const fs = require('fs')
fs.makedir('x/y/z', {recursive:true},(err)=>{
    if(err) {
        return console.log(err)
    }
})
fs.copyFile(...)
```

### Consola, utilidades y debugging

Aparte de la console normal, tambien tenemos un objeto console.Console. Este objeto nos permite manejar todas las funciones de consola y ademas alterar la forma a salida en la que queremos mostrar estos.

```javascript
const fs = require("fs");

const out = fs.createWriteStream("./out.log");
const err = fs.createWriteStream("./err.log");

const consoleFile = new console.Console(out, err);

setInterval(() => {
    consoleFile.log(new Date());
    consoleFile.error(new Error("Ooops!"));
}, 2000);
```
Hay otras formas de mandar mensaje aparte de console.log:
```javascript
console.info("hello world");
console.warn("hello error");

console.assert(42 == "42");
console.assert(42 === "42");

console.trace("hello");
```
Tambien podriamos incluir mensajes que solo aparecerian si estamos usando el debbug_log correcto, (el mensaje solo aparecera si usamos el comando NODE_DEBUG=foo node x.js):
```javascript
const util = require("util");
const debuglog = util.debuglog("foo");

debuglog("hello from foo");
```
Por ultimo, podemos usar el modulo 'util'.deprecate() para poder indicar que alguna funcion de nuestro proyecto esta con errores o que en una futura actualizacion podria ser eliminado.

```javascript
const util = require('util');
const x = util.deprecate(() => {
    ...
}, 'mensaje de advertencia');
x();
```
### Debuging
Podemos usar **node --inspect** para realizar un mejor debuging de nuestra aplicacion. Este comande hace que node cree un servidor deonde podremos conectarnos con cualquier navegador. Esto permite el uso de herramientas de debuging del navegador, igual como si estubieramos haciendo debuging del frontend.


### Cluster de procesos
Al igual que un cluster de bases de datos, un cluster de procesos es hacer que un proceso que este corriendo en un hilo se replique para cada hilo de procesos que tiene el cpu, todos nocetados al mismo puerto. Con esto logramos que el procesador siempres este resolviendo solicitudes de manera paralela y ,en el caso de un servidor, que todos estos procesos usen el mismo puerto para las conexiones entrantes. 