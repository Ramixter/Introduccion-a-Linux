# Lectura e interpretación de permisos

Algo fundamental en Linux es el tema de la **lectura de permisos**.

Para apoyarnos en este tema tenemos dos fuentes de información para consultar:

- [Permisos y derechos en Linux](https://blog.desdelinux.net/permisos-y-derechos-en-linux/?msclkid=22f8cb88ba8111ecb5d8a3db91f066ab)
- [Permisos básicos en Linux](https://www.profesionalreview.com/2017/01/28/permisos-basicos-linux-ubuntu-chmod/)

**El principal problema de los permisos avanzados es que a la hora de entenderlos es que los permisos se explican mal**. Vamos a intentar explicarlos lo mejor posible para que se entiendan.

vamos a crear un archivo `file.txt`; para ello hacemos uso de un nuevo comando que es el `touch`. El comando `touch` nos permite crear un archivo.

```bash
touch file.txt
```

>Si hicieramos un `cat` veríamos que este fichero estaría vacío.

Podemos meterle contenido  de varias maneras a este fichero:

- `echo`: Podemos usar el comando `echo` para meter información que queremos dentro del fichero:
   
    ```bash
    echo "Hola estamos metiendo información" > file.txt
    ```

    ```bash
    cat file.txt
    ```

   - ```
     Hola estamos metiendo información
     ```

   Si jugamos con un único redirector, nos fijamos que si escribimos otra línea con `echo` nos sobreescribiría lo anterior, por ejemplo:
   
   ```bash
   echo "Hola esto es nuevo" > file.txt
   ```

   ```bash
   cat file.txt
   ```

   - ```
     Hola esto es nuevo
     ```
   
   Es decir, no nos hace un `apend`, es decir, no nos pone una información detrás de otra de forma apilonada.

   **Si queremos que no nos sobreescriba la data ya existente usaremos un doble redirector `>>`**

    ```bash
    echo "Hola seguimos añadiendo información" >> file.txt
    ```

    ```bash
    cat file.txt
    ```
    
   - ```
     Hola esto es nuevo
     Hola seguimos añadiendo información"
     ```

- `nano`: con el comando `nano` lo que realmente abrimos es un editor de texto de Linux donde podemos meter el contenido escribiéndolo nosotros mismo.

    ```bash
    nano file.txt
    ```

- `vi`: con este comando abrimos el editor `vi` que es otro de los editores de texto que tiene Linux. Este editor es más complejo que el `nano` pero a su vez es mucho más potente si se aprende a manejar.

    ```bash
    vi file.txt
    ```

Ahora vamos a hacer un `ls -l` para ver la estructura que tiene nuestro fichero `file.txt`:

```bash
ls -l
```

   - ```
     -rw-r--r-- 1 ramiro ramiro   57 sep 29 17:30 file.txt
     ```

Y ahora lo que tenemos que hacer es interpretar lo que esta ocurreindo por pantalla. Si nos fijamos en la primera parte vemos que tenemos lo siguiente:

```bash
-rw-r--r-- 
```

Esto lo tenemos que dividir en 3 partes, más o menos sería lo siguiente

<table class="schedule-table" cellpadding="0" cellspacing="0">

