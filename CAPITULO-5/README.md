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