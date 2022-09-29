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
file file
```

>file: empty

```bash
file #nombre_del_fichero
```

Si le hacemos un `cat` al fichero `file` veremos que está vacío.

**¿Cuál es la idea?**

Pues ahora mismo estamos empleando un **descriptor de archivo** identificado con el número 3. Si ahora por ejemplo queremos comunicarnos con ese director de archivo, el cual en este caso estamos empleando un descriptor de archivo con capacidad de lectura y escritura.

  - Si quisiera solamente lectura le ponemos solamente un `<`
      ```bash
      exec < file # only read
      ```
  - Si quisiera solamente escritura le pones solamente un `>`
      ```bash
      exec > file # only write
      ```