# Cuestionario de control de flujo y operadores

## Pregunta 1 / 8

¿Sabrías decir qué es lo que está pasando aquí?

```bash
> exec 3<> file
> exec 4>&3
> whoami >&4
> exec 4>&-
> exec 3>&-
```

- Se comienza utilizando un descriptor de archivo con capacidad de lectura y escritura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo

- Se comienza utilizando un descriptor de archivo con capacidad de lectura y escritura para posteriormente crear una copia de este cerrando el descriptor de archivo previamente creado al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo.

- Se comienza utilizando un descriptor de archivo con capacidad de lectura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo

- Se comienza utilizando un descriptor de archivo con capacidad de escritura para posteriormente crear una copia del descriptor de archivo al número 4. Al enviar el output del comando, se almacenará en el mismo archivo 'file' y posteriormente se cierran ambos descriptores de archivo