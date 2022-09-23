# INTRODUCCÍON

## Introduccion a Linux

Vamos a ver algunas nociones de lo que Linux y su entorno nos puede ofrecer, así como por ejemplo los distintos comandos con los que podemos estar trabajando.

Vamos a trabajar con **Sistemas Operativo**. Un **Sistema Operativo** es un programa o un conjunto de programas de un sistema informático, que administra los recursos físicos (la parte hardware), los protocolos de ejecución del resto de contenido (la parte software), así como la interfaz de usuario.

Por ejemplo, Ubuntu, Windows, MacOS son sistemas operativos entre otros.

Nosotros vamos a ver 2 sistemas operativos orientados al **Pentesting** ya que veremos un enfoque un poco más práctico en la parte de la **Ciberseguridad**.

Podemos usar la distribución de **[Ubuntu](https://ubuntu.com/download/desktop)**, o podemos descargarnos los siguientes sistemas operativos:

- **[Parrot](https://parrotsec.org/)**: este SO es que el vamos a estar usando de ahora en adelante para nuestro aprendizaje. Usaremos el `Parrot Security Edition`.

- **[Kali Linux](https://www.kali.org/get-kali/)**: muy conocido en el ambito de la Ciberseguridad.

Tanto `Parrot` como `Kali Linux` van a ser una buena opción a la hora de usar herramientas de pentesting, ejecutar y desplegar ataques.

> Da igual que tipo de distibución usemos, cualquiera de ellas nos va a ser útil a la hora de realizar el aprendizaje del manejo de Linux, así que sientete libre de usar la que quieras.

Nos descargaremos la imagen `.ISO` del SO que vayamos a usar y lo instalaremos en un entorno de virtualización.

## Crear una máquina virtual.

Una vez tenemos nuestra imagen `.ISO` del SO que vayamos a utilizar vamos a **Virtualizar** una máquina sobre la cual instalaremos nuestro SO.

Para ello haremos uso de un **Hipervisor**, como son por ejemplo **[VirtualBox](https://www.virtualbox.org/)** o **[VMware](https://www.vmware.com/es/products/workstation-pro/workstation-pro-evaluation.html)** que son los más conocidos y los que la mayoría de gente utiliza tanto para aprender como para trabajos profesionales. Hay otros como por ejemplo **Proxmox** o **Hyper-V** que también son conocidos para el uso de máquinas virtuales.

Pues para empezar vamos a usar un Hipervisor para virtualizar nuestra primera máquina virtual.

| VirtualBox  | VMware |
| :---:  | :---:  |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000001.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000008.png)   |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000002.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000009.png)  |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000003.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000010.png)  |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000004.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000011.png)  |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000005.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000012.png)  |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000006.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000013.png)  |
| ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000007.png)  | ![img](/INTRODUCCION/imagenes/Window-WRADMIN-000014.png)  |

> Estas configuraciones se deben revisar dependeindo de las características que queramos asignarles a cada máquina y para la función a la que vayan destinadas, mirando por ejemplo la memoría RAM, los núcleos y procesadores, la tarjeta de red, etc.

## Instalación del Sistema Operativo (Parrot Security Edition )

Dependiendo del sistema operativo que vayamos a instalar lo haremos de distintas maneras, en este caso recordemos que nosotros vamos a trabajar con **Parrot**, por lo que en este ejemplo veremos la instalación de este SO.

Para instalar Parrot SO vamos a seguir los siguientes pasos y la sigueinte configuración:



