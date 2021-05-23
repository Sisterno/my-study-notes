# Typescript
### Por que estudiar Typescript?
En un proyecto me dijeron que con typescript te puedes evitar un monton de errores que van a aparecer por no validar tus datos. Tambien que si ya habia utilizado lenguajes fuertemente tipados como javascript o c#, typescript me iba a ser facil de entender. Asi que con esas estamos.

### Instalacion
Para instalar typescript de manera global:
```node
npm install -g typescript
```
Algunos comandos de typescript son:
*tsc -v* -> Version de TS
*tsc 'archivo.ts'* -> Compilar  el archivo TS y crea un archivo JS
*tsc --watch '/x/y'* -> Proceso que al cambiar un archivo de los que tu indiques, realiza automatica la copilacion

### Configuracion
*tsc --init* -> Inicializa TS , crea un archivo tsconfig.json
Segun las configuracion que se tenga en el archivo tsconfig.json, se puede usar simplemente *tsc* y se ejecutara.

### Tipeado
La utilidad de TS se vasa en el uso de tipos de variables. Esta validacion permite corregir el 15% de errores comunes que se dan en JS, por eso existe.

Hay 2 formas de dar un tipo a una variables, de manera implicita o de manera explicita.
```ts
let x:number // Manera expplicita

let x=5 // Manera implicita
```
Algunos tipos basicos de varibles son: 
```ts
let x:number
let x:string
let x:boolean
let x:hexa

```
