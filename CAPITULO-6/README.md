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

Esto lo tenemos que dividir en partes, más o menos sería lo siguiente, donde tenemos que tener clara que la secuencia siempre será **`rwx`**.

| Tipo de archivo| Propietario | Grupos | Otros|
| :---: | :---:       |    :---:    |     :---: |
| `-` | `rw-`   | `r--`    | `r--`  |

Donde ahora vamos a separarlo y a verlo desde los distintos puntos de vista en cuanto a información nos ofrece todo esto.

| Read - Lectura | Write - Escritura | Execute - Ejecutar|
| :---:        |     :---:      |          :---: |
| `r`   | `w`     | `x`    |

Ahora estamos hablando de **propietario**, de **grupos** y de **otros**. Por lo que ¿cómo sabemos esas características en el fichero?¿o dónde lo podemos mirar?

Pues la maneara de saber cuál es el propietario y el grupo al que pertenece el fichero es con el `ls -l`

```bash
ls -l
```

   - ```
     -rw-r--r-- 1 ramiro ramiro   57 sep 29 17:30 file.txt
     ```

El primer nombre que nos aparece es el del **propietario**, mientras que el segundo es el del **grupo** al que pertenece el fichero. **Recordemos que cada usuario tiene un grupo asignado con su mismo nombre**.

**La prioridad en cuanto a permisos la marca la jerarquía de: **Propietario > Grupo > Otros**. Que lo leemos de izquierda a derecha en la línea de comandos**

Ahora vamos a interpretar lo que dice cada apartado de los permisos dividido por partes. En nuestro caso recordemos que teníamos la siguiente división:

| Tipo de archivo| Propietario | Grupos | Otros|
| :---: | :---:       |    :---:    |     :---: |
| `-` | `rw-`   | `r--`    | `r--`  |

De donde podemos leer más información aún.

|      | Tipo de archivo| Propietario | Grupos | Otros|
|   :---:   | :---: | :---:       |    :---:    |     :---: |
|      | `-` | `rw-`   | `r--`    | `r--`  |


<table style="width: 100%; text-align: center;">
  <tr>
    <td></td>
    <td>Tipo de archivo</td>
    <td>Propietario</td>
    <td>Grupos</td>
    <td>Otros</td>
  </tr>
  <tr>
    <td></td>
    <td><p><code>-</code></p></td>
    <td><p><code>rw-</code></p></td>
    <td><p><code>r--</code></p></td>
    <td><p><code>r--</code></p></td>
  </tr>
  <tr>
    <td>Características</td>
    <td><ul><li><p><code>-</code>: fichero</p></li><li></li></ul></td>
  </tr>
</table>