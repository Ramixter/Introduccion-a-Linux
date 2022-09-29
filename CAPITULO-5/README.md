# Cuestionario de control de flujo y operadores

## Pregunta 1 / 8 - ¿Sabrías decir qué es lo que está pasando aquí?

```bash
exec 3<> file
exec 4>&3
whoami >&4
exec 4>&-
exec 3>&-
```

- [ ] Se comienza utilizando un descriptor de archivo con capacidad de lectura y escritura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo

- [ ] Se comienza utilizando un descriptor de archivo con capacidad de lectura y escritura para posteriormente crear una copia de este cerrando el descriptor de archivo previamente creado al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo.

- [ ] Se comienza utilizando un descriptor de archivo con capacidad de lectura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo

- [ ] Se comienza utilizando un descriptor de archivo con capacidad de escritura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo

<details>
<summary>Solución</summary>
  
- [x] Se comienza utilizando un descriptor de archivo con capacidad de lectura y escritura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo

   >La operación `exec 4>&3` crea un descriptor de archivo `4` el cual actúa como copia del descriptor de archivo `3`. En caso de haber querido cerrar el primer descriptor tras establecer la copia, podríamos haber hecho `exec 4>&3-`.
   
</details>

## Pregunta 2 / 8 - ¿Cómo puedo redirigir el output de un comando a un archivo? **(varias respuestas)**

- [ ] whoami file
- [ ] whoami | file
- [ ] whoami > file
- [ ] (whoami &>/dev/null) > file
- [ ] whoami 1> file

<details>
<summary>Solución</summary>
  
- [x] whoami > file

   >Este comando redirige el standard output (`stdout`) a un archivo.

- [ ] (whoami &>/dev/null) > file

   >Si no hubieran habido unos paréntesis, pese a no ver el output por consola, este habría sido almacenado en el archivo, pero al llevar el paréntesis lo que rediriges al archivo file es el output de ese comando ejecutado a nivel de sistema, que es un vacío, no teniendo por tanto ningún contenido el archivo `file`. Esta respuesta es incorrecta.

- [x] whoami 1> file

   > El valor 1 corresponde al descriptor de archivo por defecto para stdout, por lo tanto estaremos redirigiendo mismamente el output del comando.

</details>

## Pregunta 3 / 8 - ¿Qué se estará almacenando en el archivo ‘test’ a la hora de aplicar este comando?

```bash
whoami &> test
```

- [ ] El archivo no tendrá contenido siempre y cuando no posea stderr
- [ ] Se almacenará tanto el stderr como el stdout del comando aplicado
- [ ] Se almacenará sólo el stderr del comando aplicado
- [ ] Se almacenará sólo el stdout del comando aplicado

<details>
<summary>Solución</summary>
  
- [x] Se almacenará tanto el stderr como el stdout del comando aplicado

   >El control de flujo `&>` sirve para redirigir tanto el stderr como el `stdout` a un archivo. Otra forma de representar este mismo control de flujo sería con `> test 2>&1`

</details>

## Pregunta 4 / 8 - ¿Son estos dos controles de flujo lo mismo?

```bash
whoam > file1 2>&1

whoam &> file2

ls -l file*
-rw-r--r-- 1 ramiro ramiro 33 sep 29 16:52 file1
-rw-r--r-- 1 ramiro ramiro 33 sep 29 16:52 file2
```

- [ ] Verdadero
- [ ] Falso

<details>
<summary>Solución</summary>
  
- [x] Verdadero

   >Recuerda que el uso del operador `&>` sirve para indicar que tanto el `stderr` como el stdout va a ser redirigido a un archivo, igual que la instrucción que está previamente definida.

</details>


## Pregunta 5 / 8 ¿Cómo puedo enviar el output del comando ‘whoami’ al descriptor de archivo creado?

```bash
exec 3<> file
```

- [ ] whoami exec 3&-
- [ ] whoami 3>&1
- [ ] whoami >&3
- [ ] whoami 3<file

# ¿Cómo puedo cerrar el descriptor de archivo una vez hemos depositado el contenido deseado?


```bash
exec 3<> file
whoami >&3
cat file
```

exec 4>&3
<&3
exec 3>&1
[]exec 3>&-
end 3>&-

# ¿Qué sucederá cuando se aplique el último comando?

exec 3<> file
exec 4>&3-
whoami >$4
whoami >&3


Se volcará el output del comando 'whoami' 2 veces en el mismo archivo
Se volcará el output del comando 'whoami' en el mismo archivo, borrando lo que anteriormente existiera
Se almacenará 2 veces lo mismo dado que el descriptor de archivo 4 es una copia del descriptor 3
[]El comando causará un error, dado que el descriptor de archivo 3 ha sido cerrado

## ¿Qué estaré almacenando en el archivo ‘file’ con este comando?

```bash
whoami 2> file
```

[]Nada, dado que posee errores
El stdout
El stderr
command not found: whoam
Nada, dado que el comando no existe