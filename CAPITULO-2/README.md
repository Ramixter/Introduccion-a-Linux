# [CONTENIDO](https://github.com/Ramixter/Introduccion-a-Linux)
1. [Introducción](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#contenido)
   - [Introducción a Linux](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#introduccion-a-linux)
   - [Crear una máquina virtual](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#crear-una-m%C3%A1quina-virtual)
   - [Instalación del Sistema Operativo (Parrot Security Edition)](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#instalaci%C3%B3n-del-sistema-operativo-parrot-security-edition)
2. [Comandos de Linux](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#contenido)
   - [¿Qué usuario somos? `whoami`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#qu%C3%A9-usuario-somos-whoami)
   - [¿A qué grupo perteneces? `id`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#a-qu%C3%A9-grupo-perteneces-id)
   - [Ver el contenido de un archivo `cat`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#ver-el-contenido-de-un-archivo-cat)
   - [`which`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#which)
   - [`echo`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#echo)
   - [Aplicación de filtros](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#aplicaci%C3%B3n-de-filtros)
     - [Pipear](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#pipear)
   - [Rutas `pwd`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#rutas-pwd)
   - [Listar directorios `ls`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#listar-directorios-ls)
     - [Listas detalladas](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#listas-detalladas)
   - [Cambiar de directorio `cd`](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#cambiar-de-directorio-cd)
3. [Control del flujo stderr-stdout, operadores y procesos en segundo plano](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-3#contenido)
***

# COMANDOS BÁSICOS DE LINUX

Vamos a ver una serie de comandos de Linux y sus funciones dependiendo de lo que queramos hacery cómo nos queramos mover sobre este entorno de trabajo mediante comandos.

Aquí hay una chuleta muy útil con comandos de linux que podemos ver y nos servirá de ayuda:

- **[Chuleta comandos Python](https://ciberninjas.com/chuleta-comandos-linux/)**
- **[Comandos básicos de Linux](https://www.bonaval.com/kb/cheats-chuletas/comandos-basicos-linux)**
- **[Guía en PDF de comandos básicos de Linux:](/CAPITULO-2/sources/comandos.pdf)**

Nosotros vamos a poner aquí algunos ejemplos que vamos a estar viendo que nos ayudarán a entender mejor cómo funciona Linux y sobre todo a empezar a soltarnos dentro de este entorno que se usa a nivel profesional y que hará que tengamos una buena base a la hora de desarrollarnos profesionalmente.

Para abrir una consola podemos pulsar el comando `Windows + T` vamos a abrir una **terminal**, es decir, a la **consola** y podremos empezar a trabajar.

## ¿Qué usuario somos? `whoami`

El primer comando que vamos a ver es `whoami` que nos dirá con qué usuario estamos logeados en ma máquina o cuál es nuestro usuario.

```bash
whoami
```

> Siempre que abrimos una terminal tenemos que pensar en que eres un usuario a nivel de sistema.

Hay varios usuarios a nivel de sistema.

## ¿A qué grupo perteneces? `id`

Con el comando `id`, podemos ver a qué grupos pertenecemos. En el sistema hay una serie de grupos existentes.

```bash
id
```

**Algo a destacar, es que normalmente cada usuario tiene un grupo asignado con el mismo nombre de usuario**

Cuando estamos efectuando Pentesting, ver en todo momento en qué grupo estamos es muy interesante, porque hay algún que otro grupo que puede presentar un riesgo potencial de cara a una escalada de privilegios o alguna vulnerabilidad. Hay varios grupos peligrosos o considerados como **críticos**, como por ejemplo el grupo **docker**, o el grupo **lxd**. Hay vias potenciales a través de las cuales puedes abusar de estos grupos para escalar privilegios y convertirnos en **root**.

Pero en un principio el único que presenta riesgo en este momento es el grupo **sudo**. Nuestro usuario tiene el privilegio de convertirse en root. ¿Qué quiere decir esto?.

El echo de que estemos en el grupo sudo lo que nos permite es que al ejecutar el comando `sudo su` nos pedirá una contraseña (la contraseña de tu usuario), y así nos podemos convertir en el usuario root.

```bash
sudo su
```
Y si hemos introducido bien la contraseña si volvemos a ejecutar el comando `whoami` veremos que ahora nuesto usuario sería el usuario root.

Tenemos que considerar al usuario root como el usuario privilegiado, el que tiene mayor privilegio a nivel de sistema. Y también podemos ejecutar el comandi `id` para ver a qué grupos pertenecemos.

> Cuando en Pentesting hablamos de **rootear una máquina** es simpplemente elevar nuestro privilegio.

En cualquier momento podemos usar el comando `exit`para salir de la sesión actual en la que estamos logueados.

```bash
exit
```
Si ahora por ejemplo ya nos habíamos logueado como root en la terminal, y volvemos a ejecutar `sudo su`no nos volverña a pedir la contraseña, ya que por detrás se guarda un **token privilege**, que temporalmente durante un cierto periodo de tiempo almacena una especie de token que queda almacenado temporalmente para que no tengas que volver a poner la contrasñea.

**Pero también podemo usar el comando `sudo`para ajecutar un comando con privilegios sin necesidad de convertirme en root, por ejemplo el comando `whoami`, es decir, `sudo whoam`.** No estamos como el usuario root, lo que realmente hacemos es ejecutar el comando que queramos como root. Esto viene bien a la hora de ejecutar comandos como root sin ser el usuario root.

Cada grupo que hemos visualizado con el comando `id` los podemos ver en la siguiente ruta en el sitema: `/etc/group` (que es uno de los distintos directorios que existen). Y nos vendrá bien saber para qué se usa o qué contiene cada ruta. Esta ruta, `/etc/group`, es un archivo, realmente es un directorio.

## Ver el contenido de un archivo `cat`

Ahora por ejemplo si usamos el oomando `cat` junto con la ruta `/etc/group` podemos ver el contenido.

```bash
cat
```

```bash
cat /etc/group
```
Aquí veremos todos los grupos ecistentes y el identificador al final.

**Para movernos dentro de un fichero de una manera más rapida y cómoda podemos usar los botones del teclado `Av Pág`(hacia abajo) y `Re Pág`(hacia arriba). O simplemente con las flechas de dirección.**

## `which`

El comando `which` nos ayudará a saber más sobre ciertos comandos, como por ejemplo el comando `cat`

```bash
whhich
```

```bash
which cat
```
>/usr/bin/cat

Podemos ver como nuestro comando `cat` está enlazado por un alias a una ruta. **Hay una distinción que tenemos que tener en cuenta que son `rutas absolutas` y `rutas relativas`.**

**Cuando ejuecutamos un comando, como por ejemplo `whoami` lo que estamos haciendo es la ejecución de un binario mediante una `ruta relativa`, es decir, no hemos tenido que especificar su ruta absoluta. Cada binario debería de tener una `ruta absoluta` que la podemos ver con `which`.**

Por ejemplo ¿en qué `ruta absoluta` está el binario `whoami`?

```bash
which whoami
```
>/usr/bin/whoami

Entonces vemos una cosa curiosa, nos podemos dar cuenta que si usamos en nuestra terminal el comando `whoami` y el comando `/usr/bin/whoami` es lo mismo, es decir, daría igual si usamos cualquiera de los dos comandos, el resultado será el mismo:

```bash
whoami
```
```bash
/usr/bin/whoami
```

**Algo a tener en cuenta es que hay ocasiones en las que logremos a través de una página web ejecutar comandos de forma remota. Imaginemos que logramos hacer una inyección, hay ocasiones en las que a lo mejor queremos ejecutar ciertos comandos, pero es preferible validar de primeras si el comando existe. Por eso es tan útil el `which whoami`, porque si me reporta la web la `ruta absoluta` se que el binario existe** Si ponemos `wich` y algo que no exista nos reportará un `not found`.

**Hay ocasiones en las que `which` no existe, en este caso hay otra alternativa que sería `command -v`**

```bash
command -v whoami
```
>/usr/bin/whoami

Entonces nos podemos preguntar ¿y por qué sabe que `whoami` está en `/usr/bin`?

Pues es porque hay una variable de entorno que existen que para ver su contenido tiene que ir acompañadas del símbolo **`$`**, por ejemplo: `$PATH`.

## `echo`

El comando `echo` nos permite imprimir el resultado que queramos por pantalla, es decir por la terminal, por ejemplo si usamos `echo` seguido de una cadena de texto podemos ver cómo nos aparece dicha cadena de texto en nuestra terminal.

```bash
echo Estamos aprendiendo Linux
```
>Estamos aprendiendo Linux

 O incluso podemos sacar más información usando la convinaciñon de varios comandos de la manera adecuada para ver dicha información por pantalla, por ejempolo, vamos a ver el uso de `echo` junto a la variable de entorno `$PATH`.

```bash
echo $PATH
```
>/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/usr/share/games:/usr/local/sbin:/usr/sbin:/sbin:/home/ramiro/.local/bin:/snap/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games

Vemos varias rutas separadas por dos puntos. Lo que vemos es como un orden de prioridad existente a través del cual cuando tú ejecutas un comando, primero comienza buscando dicho comando en la primera ruta de `$PATH`y así de manera recursiva en orden hasta encontrarlo en alguna de las rutas de `$PATH`.

>Podemos "retocar" nuestro `$PATH`. Veremos técnicas de hacking en los módulos de pentesting que se llaman **path hijacking**, a través del cual puedes ejecutar un secuetro del `$PATH` y escalar privilegios y liarla para que el flujo del programa funcione u opere de otra forma. Secuestras el `$PATH` para cambiar un binario mencionado de forma relativa a una absoluta, etc.

**Un comando básico y muy útil cuando estemos escribinedo en pantlla es el comando `Ctrl + L` para limpiar la pantalla**

## Aplicación de filtros

Hay situaciones en las que queremos filtrar el contenido de un `output` para ver solamente la información necesaria sin que el resto de información del fichero aparezca por pantalla. Para ello lo mejor es aplicar un filtro. 

Nosotros cuando queramos operar sobre un **output**, por ejemplo por el ocmando `cat /etc/group` para filtrar la información que queremos lo que podemos hacer es **PIPEAR**

### Pipear

**Pipear** es como decir que queremos el output del comando anterior ejecutado queremos tratarlo para efectuar una segunda operatoria. Hay un comando en Linux que es el comando `grep` (que es muy usado) que sirve para aplicar filtros.

Por ejemplo vamos a filtrar el output del comando `cat /etc/group` por la palabra "floppy", entonces vamos a hacer uso de `grep`:

```bash
cat /etc/group | grep "floppy"
```
>floppy:x:25:ramiro

Que nos dará como resultado, reporte, la línea de todo el archivo donde está la palabra "floppy" puesta. Si además queremos ver la línea donde se encuentra lo que hemos buscado en el fichero, podemos usar el atributo `-n` junto a `grep`para mostrarnos la línea del fichero en la que se encuentra.

```bash
cat /etc/group | grep "floppy" -n
```
>19:floppy:x:25:ramiro

## Rutas `pwd`

El comando `pwd` nos servirá para ver la ruta en la que nos encontramos en ese momento, es decir, que si cambiamos de ruta, el `pwd`nos dará un resultado distinto en cada ocasión que nos movamos de una ruta a otra.

```bash
pwd
```
>/home/ramiro

## Listar directorios `ls`

Si dentro de nuestro directorio, o en el directorio que nos encontremos ejecutamos el comando `ls` veremos el contenido del directorio donde nos encontremos. Econtraremos directorios, archivos y ficheros.

```bash
ls
```

`ls` es otro alias

```bash
which ls
```
>/usr/bin/ls

Si por ejemplo queremos listar el contendi ode un directorio distinto lo podemos hacer usando `ls` junto a la `ruta`, por ejemplo:

```bash
ls /bin
```

### Listas detalladas:

Podemos usar el contenido de un directorio de manera más detallada, para ello podemos usar distintos atributos junto al comando `ls`

- `-l`: este atributo nos permitirá ver listado con detalle el contenido del directorio que queramos:

```bash
ls -l
```
## Cambiar de directorio `cd`

El comando `cd` viene de "change directory", es decir, cambbio de directorio. Podemos navegar a través de directorios con este comando.

- `..`: vamos al directorio padre, es decir, al directorio que es el contenedor del directorio actual.
- `ruta`: vamos a la ruta que especificamos.
- `\`: nos iremos a la raiz, a la raiz del sistema operativo.

Si usamos simplemte el comando `cd` nos llevará al directorio de trabajo por defecto que tenemos para nuestro usuario, al directorio presonal del usuario.

```bash
cd
```

> Recuerda que siempre puedes saber en que ruta estás usando el coamndo `pwd`.

Recordando las variables de entorno, podemos ver una variable de entorno que almacena el directorio de trabajo, esa variable es `$HOME`.

```bash
echo $HOME
```
>/home/ramiro

¿Dónde se definen, además de los usuarios existentes a nivel de sistema, los directorios personales de usuarios?

Hay un archivo a nivel de sistema que es el `/etc/passwd`. Si lo abirmos, `cat /etc/passwd`, veremos un listado de líneas de código donnde podemos ver:
- el usuario
- el identificador de usuario, `id`
- el identificador de grupo
- el nombre del usuario
- el directorio personal
- el tipo de `SHELL` que usa el usuario

```bash
cat /etc/passwd
```

Hay otra variable de entorno que nos interesa conocer que es `$SHELL`, donde veremos en todo momento el tipo de `SHELL` que estás utilizando.

Los tipos de ``SHELL` se ven en: `cat /etc/shells`.

```bash
cat /etc/shells
```

[:arrow_up_small:Volver al inicio](#contenido) | [3. Comandos de Linux:arrow_forward:](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#contenido)