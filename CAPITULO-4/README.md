# [CONTENIDO](https://github.com/Ramixter/Introduccion-a-Linux)

1. [Introducción](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#contenido)

    <details>
    <summary>Resumen</summary>
  
    - [Introducción a Linux](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#introduccion-a-linux)
    - [Crear una máquina virtual](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#crear-una-m%C3%A1quina-virtual)
    - [Instalación del Sistema Operativo (Parrot Security Edition)](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-1#instalaci%C3%B3n-del-sistema-operativo-parrot-security-edition)
   
    </details>
  
2. [Comandos de Linux](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-2#contenido)

    <details>
    <summary>Resumen</summary>
  
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
   
    </details>
   
3. [Control del flujo stderr-stdout, operadores y procesos en segundo plano](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-3#contenido)


4. [Descriptores de archivo](https://github.com/Ramixter/Introduccion-a-Linux/tree/main/CAPITULO-4)

***

# Descriptores de archivo

Vamos a hablar acerca de las redirecciones en `Bash` empleando descriptores de archivos. Esto realmente no es que se utilice mucho, y en scripting en `Bash` tampoco. Pero a nivel de cultura general hay que conocerlo y *pilotarlo*.

## `exec`

Si por ejemplo ejecutamos el comando `exec` podemos crear un fichero. Creamos un archivo `file`.

```bash
exec 3<> file
```

>Si hacemos `ls` podemos ver el fichero `file` creado.

>No usamos el `2` sino el `3` porque recordemos que el `2` es el error.

## `file`

Para saber que tipo de fichero usamos el comando `file`, podemos ver de que tipo de fichero se trata.

```bash
file file # second file is the name of the file or directory
```
- ```
  file: empty
  ```


Si le hacemos un `cat` al fichero `file` veremos que está vacío.

**¿Cuál es la idea?**

Pues ahora mismo estamos empleando un **descriptor de archivo** identificado con el número 3. Si ahora por ejemplo queremos comunicarnos con ese director de archivo, el cual en este caso estamos empleando un descriptor de archivo con capacidad de lectura y escritura.

  - Si quisiera solamente lectura le ponemos solamente un `<`
      ```bash
      exec 3< file # only read
      ```
  - Si quisiera poder escribir le pones solamente un `>`
      ```bash
      exec 3> file # only write
      ```
## Almacenar outputs

Si por ejemplo queremos hacer que el ouput de un comando se almacene en el descriptor de archivo `3` que tiene capacidad de escritura, es decir, en el archivo `file`, entonces si ejecutamos `>&3` esta es una forma de mandar el output a ese descriptor de archivo

```bash
whoami >&3
```

Esta ejecución de lineas van a ir almacenando en formato `append`, es decir, cualquier cosa que metamos se irá almacenando sin aplastar lo anterior. Lo introduce a continuación.

Se ejecutará la acción y no veremos nada por pantalla, pero para ver el contenido del fichero `file` podemos usar por ejemplo el `cat`, el output se habría almacenado en ese archivo.

```bash
cat file
```

Cuando queremos cerrar un descriptor de archivo creado, podemos jugar con el `exec`, para por ejemplo indicar el descriptor de archivo y decirle que se cierre usando `-`.

```bash
exec 3>&-
```

Esto no quiere decir que el archivo haya perdido su contenido, sino que lo que quiere decir es que de cara a un futuro output que queramos almacenar en ese descriptor de archivo nos va a decir que `bad file descriptor` o `Descriptor de fihcero erróneo`

```bash
ls >&3
```

- ```
  bash: 3: bad file descriptor
  ```

Hemos visto cuál sería la forma de cerrar un descriptor de archivos, pero se pueden jugar de varias formas, por ejemplo:

Vamos a crearnos un descriptor de archivo `5` con capcidad de lectura `<` y escritura `>` en el archivo `data`:

```bash
exec 5<> data
```

**Cosas a tener en cuenta**

Si ahora por ejemplo metemos `whoami` en el descriptor de archivo:

```bash
whoami >&5
```

```bash
cat data
```

- ```
  ramiro
  ```

Pues podemos creear copias entre descriptores de archivos. Si ahora por ejemplo hacemos ` exec 8>&5`, lo que le estamos indicando de esta forma es que lo que hay en el descriptor de archivo `5` queremos crear una copia para el descriptor de archivo `8` que estamos creando ahora

```bash
exec 8>&5
```
>Se crea la copia del descriptor de archivo `5` al `8`.

Entonces si ahora escribimos en el descriptor de archivo inicial, el `5`, por ejemplo metemos `pwd >&5`

```bash
pwd >&5
```

```bash
cat data
```

- ```
  ramiro
  /home/ramiro
  ```

Pero ahora como también el descriptor de archivo `8` es una copia del `5`, entonces cualquier cosa que metamos en el descriptor de archivo `8` se irá a ese descriptor de archivo, pero la información se meterá en el fichero `data` (hacer `cat data` para comprobarlo).

```bash
who -q >&8
```

```bash
cat data
```

- ```
  ramiro
  /home/ramiro
  ramiro
  Nº de usuarios=1
  ```

Entonces podemos hacer copias de los descriptores de archivos y luego podemos cerrar el que nosotros queramos.

Por ejemplo con el comando `exec` le podemos decir que queremos cerrar el descriptor de archivo `5`, entonces ejecutamos `exec 5>&-`. Y ahora tenemos el mismo archivo `data`. Entonces de cara a meter o incorporar un nuevo dato, por ejemplo `cat /etc/hosts >&5`y nos va a dar el error de `bad file descriptor` o `Descriptor de fihcero erróneo`, que ahora en tal caso sería el `8`que sería el que estaría funcionando.

```bash
exec 5>&-
```

```bash
cat /etc/hosts >&5
```

- ```
  bash: 5: bad file descriptor
  ```

```bash
cat /etc/hosts >&8
```

```bash
cat data
```

- ```
  ramiro
  /home/ramiro
  ramiro
  Nº de usuarios=1
  # Host addresses
  127.0.0.1  localhost
  127.0.1.1  parrot
  ::1        localhost ip6-localhost ip6-loopback
  ff02::1    ip6-allnodes
  ff02::2    ip6-allrouters
  ```

>Se pueden crear copias de otra forma, de la siguiente manera, por ejemplo, si queremos crear una copia del descriptor de archivo `8`.

En vez de crear un descriptor de archivos de lectura `<` y escritura `>` para meter datos, luego crear una copia del primer descriptor de archivo creado y luego intoducir datos en el segundo habiendo cerrado el primero sin ningún problema.

Imaginemos que creamos un descriptor de archivos con capacidad de lectura `<` y escritura `>` en el fichero `example`, entonces cualquier cosa que metamos en ese descriptor de archivos va a corresponder al fichero `example`. 

```bash
exec 5<> example
```

Imaginemos ahora que creamos una copia.

```bash
exec 6>&5
```

Tenemos ahora un descriptor de archivo `6` que es una copia del `5`. **Pero si le pones un `-` al final, cerramos el `5`**

Recordemos que los descriptores de arvhivos no son algo que se usen demasiado, pero que está bien saberlo.

**Dejamos material de apoyo para poder consultar ciertas funciones y poder aplicarlas: [Bash Redirections Cheat Sheet](/CAPITULO-4/sources/bash-redirections-cheat-sheet.pdf)**