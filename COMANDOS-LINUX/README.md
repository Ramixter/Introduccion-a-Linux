# Comandos básicos de Linux

Vamos a ver una serie de comandos de Linux y sus funciones dependiendo de lo que queramos hacery cómo nos queramos mover sobre este entorno de trabajo mediante comandos.

Aquí hay una chuleta muy útil con comandos de linux que podemos ver y nos servirá de ayuda: **[Chuleta comandos Python](https://ciberninjas.com/chuleta-comandos-linux/)**

Nosotros vamos a poner aquí algunos ejemplos que vamos a estar viendo que nos ayudarán a entender mejor cómo funciona Linux y sobre todo a empezar a soltarnos dentro de este entorno que se usa a nivel profesional y que hará que tengamos una buena base a la hora de desarrollarnos profesionalmente.

Para abrir una consola podemos pulsar el comando `Windows + T` vamos a abrir una **terminal**, es decir, a la **consola** y podremos empezar a trabajar.

## ¿Qué usuario somos?

El primer comando que vamos a ver es `whoami` que nos dirá con qué usuario estamos logeados en ma máquina o cuál es nuestro usuario.

```bash
whoami
```

> Siempre que abrimos una terminal tenemos que pensar en que eres un usuario a nivel de sistema.

Hay varios usuarios a nivel de sistema.

## ¿A qué grupo perteneces?

Con el comando `id`, podemos ver a qué grupos pertenecemos. En el sistema hay una serie de grupos existentes.

```bash
id
```

**Algo a destacar, es que normalmente cada usuario tiene un grupo asignado con el mismo nombre de usuario**

Cuando estamos efectuando Pentesting, ver en todo momento en qué grupo estamos es muy interesante, porque hay algún que otro grupo que puede presentar un riesgo potencial de cara a una escalada de privilegios o alguna vulnerabilidad. Hay varios grupos peligrosos o considerados como **críticos**, como por ejemplo el grupo **docker**, o el grupo **lxd**. Hay vias potenciales a través de las cuales puedes abusar de estos grupos para escalar privilegios y convertirnos en **root**.

Pero en un principio el único que presenta riesgo en este momento es el grupo **sudo**. Nuestro usuario tiene el rpivilegio de convertirse en root. ¿Qué quiere decir esto?.

El echo de que estemos en el grupo sudo lo que nos permite es que al ejecutar el comando `sudo su` nos pedirá una contraseña (la contraseña de tu usuario), y así nos podemos convertir en el usuario root.

```bash
sudo su
```

