# Linux
## Comandos basicos
ls -> listado de archivos y directorios  
rm "" -> remove; eliminar archivos.  
> -r -> recursive; Eliminar de manera recursiva.  

touch "" "" ...n -> creacion de n archivos
mkdir "" -> creacion de directorio
- - -
## Vista de archivos de texto
head "" -> Muestra las primeras lineas del archivo.  
> -n x -> Muestra x lineas.  

tail "" -> Muestra las ultimas lineas del archivo.  
less "" -> visor de texto; reader.  
xdq-open "" -> Abrir archivo con un programa por defecto.  
nautilus -> Abre el explorador de archivos en linux.
- - -
## Camandos, info
type "comando"  -> Info de que tipo de comando es / origen / alias.  
alias "nombre del alias"="comando" -> Permite definir un alias. Si se realiza en la terminal solo estara dsiponible hasta q la terminal se cierre.  
help "comando"  -> Es igual a `"comando" --help`. Muestra informacion del comando.  
### OJO
man "comando"   -> Manual de usuario del comando, si lo tiene.  
info "comando" -> Informacion del comando.  
whatis "comando" -> Descripcion rapida del comando.  
- - -
## Wildcards
Busqueda avanzado.  
* -> Permite generalizar en la busqueda.
> `ls *.js`  
`ls *date*`

? -> Puede tomar el valor de cualquier char, solo vale por un char.
>   `ls date?.ts` -> date1.ts, date2.ts, ...

[[...]] -> Permite el uso de expresiones regulares.  
- - -
## Redireccion

"comando" > "archivo" -> Redirige el output del comando al archivo y los sobreescribe.  
"comando" >> "archivo" -> Redirige el output del comando al archivo y los concatena.  
"" > "" 2>&1 -> guarda el error
### Pipe operator
| -> Perimite redirigir el output de un comando al input de otro.  
> cowsay "hola" | lolcat  
- - -
## Operadores de control
Permiten el encadenamiento de comandos.  
; -> Ejecucion de manera sincrona.  
> comand;   
comand;  
comand;  

& -> Ejecucion de comandos asincronos.  
&& -> Ejecutar comando tras comando siempre que no se encuentre ningun error.  
|| -> Ejecucion uno tras otro; no importa si hay error.  
- - -
## Permisos
chmod "" -> Cambia los permisos de los archivos.  
whoami -> Usuario actual.  
su "" -> Cambia de usuario.  
passwd -> Cambio de contraseña.
- - -
# Variables de entorno
ln -s "" "nombre" -> Creacion de link simbolico; acceso rapido :v  
printenv -> Imprime las varibales de entorno.  
> Variables  
>> $HOME  
$PATH

.bashrc -> Archivo donde se guardan comandos o nuevas varibles el inicio de ejecucion de una terminal.   
Agregar en path
> En .bashrc , `PATH = $PATH:/home/...`
- - -
## Busqueda de archivos
find "ruta" -> Buscar :V
> -name ""  
-type f:files / d:directorios  
-size 20MB  
Se puede usar el comando exec para ejecutar una accion depues de rosolver la busqueda.  
- - -
## GREP
grep "expresion regular" "archivo"  
> -c -> count

wc "" -> word count  
>-l -> lines  
-w -> words  
-c  
- - -
## Utilidades de red
ifconfig -> Informacion de interfaces de red.  
curl "" -> Obtener data de la direccion.  
wget "" -> Resuelve peticiones y luego muestra el output.
netstat -> Informacion de la interfaz de red.
- - -
## Compresion de archivos
tar -> Compresion en formato tar y tarz
> -c -> comprimir  
-v -> verbose / mostrar output  
-f -> file  
-z -> compresion mas eficiente con gzip  
-x -> descompresion

zip "nombre" "origen" -> Comprimir
> -r -> recursive

unzip "" -> Descomprimir
- - -
## Manejo de procesos
ps -> Lista de procesos.  
top -> Procesos que usan mas recursos  
kill ""->  matar un proceso
htop -> top mejorado / debe de instalarse, no esta por defecto.
- - -
## Procesos en foreground y background  
foreground ->  Proceso q esta actualmente en ejecucion en el shell.  
background ->  Proceso q esta en ejecucion en el shell.  

jobs -> Muestra los procesos actualmente en background.  
fg "" -> Tras el proceso a foreground.  
> fg "% int" -> En caso de zsh shell

Si se usa "&" el final del comando, se manda el proceso directo a background.
- - -
## Editor de texto en la terminal
vim
> :q -> Importante; La unica forma de escapar de este agujero oscuro.  
:w -> Guardar  
i -> Pasa a modo insert.  
ESC -> Salir a modo insert.  
! -> Forzar accion
- - -

# ELminar proceso segun el puerto q esta utilizando
Matar el proceso que esta actualmente utilizando un puerto.
```linux
    fuser -k 3030/tcp
```