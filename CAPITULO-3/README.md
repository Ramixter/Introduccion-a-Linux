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

# Control del flujo stderr-stdout, operadores y procesos en segundo plano

Hay una cosa que tenemos que tener en cuenta y es que en la línea de instrucciones que nos encontramos podemos concatenar múltiples comandos. Hay una serie de operadores (`and`, `or`, `;`, etc).

>Podemos apoyarnos en los [Redirectores en Bash](/CAPITULO-3/sources/bash-redirections-cheat-sheet.pdf)

## `;`

Por ejemplo, podemos usar el comando `whoami` para saber quien soy y el comando `ls` para listar los recursos de el directorio actual de trabajo. Pero en vez de usarlos por separado, podemos concatenar estos dos comandos, por ejemplo:

```bash
whoami; ls
```

>Esto nos dice que queremos ejecutar un `whoami`, pero a la vez en el mismo *liner* podemos ejecutar el coamndo `ls`. Y podemos concaternar tantos comandos como queramos, por ejemplo: `whoami; ls; id`.

## And `&&`

Usar el `;` es una opción, pero una opción muy diferente es usar el `&&` (and). En este caso hace primero un comando y luego el siguiente.

```bash
whoami && ls
```

Y podríamos pensar que es lo mismo, que podemos usar tnato el `;`, como el `&&`. Pero realmente no, ya que el `&&` lo que hace es que el segundo operando se ejecute **si y solo si** el primer operando devuelve un código de estado exitoso. Entonces podemos ver que si el primer operando no se ejecuta de manera exitosa, no se ejecutarán los siguientes.

### Codigo de estado

El código de estado de un comando lo podemos ver de la sigueinte manera. Si por ejemplo hacemos un `cat /etc/host`, podemos ver el **código de estado** con `echo $?`, el cuál nos devolverá un número.

```bash
echo $?
```

>0

- Si nos sale un **0** significa que el **código de estado** del comando anteriormente ejecutado ha sido **EXITOSO**
- Sin embargo si es distinto de 0, entonces significa que el **código de estado** del comando es **NO EXISOTOS**.

>Hay varios códigos de estado que esxisten.

## Or `||`

Podemos usar un `||` cuando ejecutamos comandos, entonces en este caso, si el primer comando es erroneo si que nos va aejecutar el segundo operando.

Si hay un comando erroneo, nos devolverá como salida `bash: orden no encontrada` o `bash: command not found`

>Esto ya tiene que ver un poco con el tema del **Scripting en Bash**

Hay una cosa a destacar, y es que por ejemplo si ejecutamos un comando no válido nos reportará por consola `orden no encontrada` o `command not found`. Y esto es porque cuando nosotros hacemos scripts hay ocasiones en las que no nos interesa que el usuario vea errores por consola.

### Standard error `stderr`

**El error se define como `stderr`**, que se puede referenciar con el número 2. Y lo que nosotros podemos hacer es redirigir los errores. Para eso podemos decir lo siguiente `2>/dev/null`, que esto lo que quiere decir es que queremos enviar el error, el `stderr`, al `/dev/null`.

Ahora bien, ¿qué es el `/dev/null`?

Tenemos que ver el `/dev/null` como un agujero negro por así decirlo. Es un recurso existente, es un tipo de archivo especial. Cualquier cosa que enviemos al `/dev/null` hacemos que se desvanezca, en definitiva, que desaparece. Si movemos un archivo al `/dev/null` y desaparece. Esto es lo único que tenemos que tener en cuenta.

Entonces ahora supongamos que si ejecutamos un comando no exitoso, por ejemplo `whoam 2>/dev/null`, lo que estamos haciendo es que el output no exitoso de errores lo voy a redirigir a esa ruta para que no veamos el output. **Pero hay que tener en cuenta que el comando se está ejecutando**.

```bash
whoam 2>/dev/null
```

Pero si por ejemplo ejecutamos el comando `whoami 2>/dev/null` si que se ejecutará el comando `whoami`, ya que con el `2` lo que estamos indicando es que no nos muestre los errores.

```bash
whoami 2>/dev/null
```
>ramiro

Esta sería una forma de que si algo no existe, nos cercioramos de que no van a haber errores por consola, pero en caso de que exista la ejecución si que la veremos, por ejemplo:

```bash
cat /etc/host 2>/dev/null  # with errors
```

```bash
cat /etc/hosts 2>/dev/null # without errors
```

Entonces en caso de haber errores no se mostrarán por pantalla, pero en caso de no haberlos si que nos mostrará el resultado por pantalla.

Por otro lado, algo que podríamos hacer también es redirigir el `stdout` (que es lo que se muestra por pantalla), tendríamos varias formas de hacerlo:

 - **Forma rara**: lo que podemos hacer es que todo el flujo del programa se redirija al `/dev/null`, de forma que lo ejecutamos y no vemos nada, pero el inconveniente es que si tenemos una ejecución no exitosa si que nos aparecería el error por pantalla. Por que este no sería el output del comando ejecutado, esto sería un error porque el directorio o archivo no existe:

 ```bash
 cat /etc/host >/dev/null  # with errors
 ```

 ```bash
 cat /etc/hosts >/dev/null # without errors
 ```

 Algo que se suele hacer además que el output lo redirijamos al `/dev/null`es que el `stderr`, que los errores, pues los convirtamos a `stdout`, que es una forma de indicar que ahora los errores van a formar parte del `stdout` para que lo tome como output del propio comando ejecutado a nivel de sistema, el output normal, y que lo redirija al `/dev/null`. Entonces ahora ni los errores tampoco los vamos a ver, el comando se va a ejecutar, pero no vamos a ver nada.

 ```bash
 cat /etc/host >/dev/null 2>&1 # with errors
 ```

 ```bash
 cat /etc/hosts >/dev/null 2>&1 # without errors
 ```

 - **Forma "convencional"**: la forma que podemos hacerlo es poniendo simplemente el `&` y lo redirigimos al `/dev/null`, de esta forma tnato el `stdout` como el `stderr` no se van a mostrar.

 ```bash
 cat /etc/hosts &>/dev/null
 ```

**Y ahora nos podemos preguntar ¿por qué ibamos a querer ocultar el output de un programa?**

Pues por ejemplo imaginemos usamos un programa que se llama `wireshark`, veremos por pantalla el output del propio programa. Y hay veces que a lo mejor creamos scripts donde no queremos listar o mostrar el output de una herramienta que vayamos a ejecutar cierto procedimiento. A lo mejor este output nos interesa ocultarlo. Entonces como no queremos que se vea nada por pantalla lo redirigimos al `/dev/null`, ya que lo único que queremos es que nos abra el aplicativo. Tenemos el progama corriendo y no veremos nada por pantalla.

```bash
whireshark &>/dev/null
```

>El proceso de `whireshark` es un proceso *hijo*, es decir, que está ligado a nuestra terminal, en la consola actual en la que estamos.

Si queremos poner aplicativos en segundo plano, lo que podemos hacer es poner un `&` al final.

```bash
whireshark &>/dev/null &
```

```bash
whoami &>/dev/null &
```
>[1] 60712

Entonces como el output y los errores no se ven, le podemos dar al `enter`, pero como lo hemos puesto en segundo plano, lo que veremos por pantalla un número que es el `pid`, que el `pid` es el número identificativo que relaciona haciendo referencia a un proceso que esté ejecutándose en el sistema.

**Cada proceso tiene un `pid`, un valor identificativo que representa y distingue un proceso de forma unívoca.**

>Dos procesos no pueden compartir el mismo `pid`.

**¿Cómo podemos remediar que un proceso abierto por consola no se cierre al cerrar la terminal?**

Nosotros normalmente cuando queramos independizar un proceso para que no dependa del recuso principal, hacemos lo mismo que hemos visto, pero al final le metemos un `disown`. De manera que si cerramos el proceso padre, el proceso que habíamos abierto permanecería ejecutandose todavía.

```bash
whireshark &>/dev/null & disown
```
