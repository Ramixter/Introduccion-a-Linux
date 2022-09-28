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

Por ejemplo, podemos usar el comando `whoami` para saber quien soy y el comando `ls` para listar los recursos de el directorio actual de trabajo. Pero en vez de usarlos por separado, podemos concatenar estos dos comandos, por ejemplo:

```bash
whoami; ls
```

>Esto nos dice que queremos ejecutar un `whoami`, pero a la vez en el mismo *liner* podemos ejecutar el coamndo `ls`. Y podemos concaternar tantos comandos como queramos, por ejemplo: `whoami; ls; id`.

Usar el `;` es una opción, pero una opción muy diferente es usar el `&&` (and). En este caso hace primero un comando y luego el siguiente.

```bash
whoami && ls
```

Y podríamos pensar que es lo mismo, que podemos usar tnato el `;`, como el `&&`. Pero realmente no, ya que el `&&` lo que hace es que el segundo operando se ejecute **si y solo si** el primer operando devuelve un código de estado exitoso. Entonces podemos ver que si el primer operando no se ejecuta de manera exitosa, no se ejecutarán los siguientes.

## Codigo de estado

El código de estado de un comando lo podemos ver de la sigueinte manera. Si por ejemplo hacemos un `cat /etc/host`, podemos ver el **código de estado** con `echo $?`, el cuál nos devolverá un número.

```bash
echo $?
```

```
0
```