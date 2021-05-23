# Notas sobre git y github 

### .gitignore
En esta archivo se encuentra en la raiz de nuestro repositorio. En el tenemos escrito las direcciones, archivos o carpetas que queremos que git no rastreee.

!! importante
Es recomendable usar gitignore.io para la genereacion del archivo .gitignore . Esta pagina permite crear un archivo git ignore por defecto segun parametros que tu le indiques como tecnologias a usar, sistema operativo, etc.


### Comandos para algunos casos q me encontre

Cuando tengas que traer archivos de otra rama para fucionarlos con las rama actual lo puedes hacer con el checkout. En este caso tuve q traerme la docmentacion que tenia en otra rama sin tener q traer cambios no comprobados.
```git
git checkout 'realtime-chat(no-redis)' ./docs
```