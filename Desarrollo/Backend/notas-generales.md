# Notas sobre desarrollo de backend

## Informacion del sistema operativo

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
Tambien se puede ralizar el manje de directorios y archivos con el modulo 'fs':

```javascript
const fs = require('fs')
```