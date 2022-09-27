# CONTENIDO

1. [Introducción](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/INTRODUCCION#contenido)
2. [Comandos de Linux](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/COMANDOS-LINUX#contenido)
3. Scripting en Bash

***

# COMANDOS BÁSICOS DE LINUX



Vamos a ver una serie de comandos de Linux y sus funciones dependiendo de lo que queramos hacery cómo nos queramos mover sobre este entorno de trabajo mediante comandos.

Aquí hay una chuleta muy útil con comandos de linux que podemos ver y nos servirá de ayuda: **[Chuleta comandos Python](https://ciberninjas.com/chuleta-comandos-linux/)**

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

## which

El comando `which` nos ayudará a saber más sobre ciertos comandos, como por ejemplo el comando `cat`

```bash
whhich
```

```bash
which cat
```

Podemos ver como nuestro comando `cat` está enlazado por un alias a una ruta. **Hay una distinción que tenemos que tener en cuenta que son `rutas absolutas` y `rutas relativas`.**

**Cuando ejuecutamos un comando, como por ejemplo `whoami` lo que estamos haciendo es la ejecución de un binario mediante una `ruta relativa`, es decir, no hemos tenido que especificar su ruta absoluta. Cada binario debería de tener una `ruta absoluta` que la podemos ver con `which`.

Por ejemplo ¿en qué `ruta absoluta` está el binario `whoami`?

```bash
which whoami
```

