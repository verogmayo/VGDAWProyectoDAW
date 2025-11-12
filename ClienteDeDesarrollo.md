[Volver al menu principal](README.md)

# CLIENTE DE DESARROLLO
|  DAW/DWES Tema2 |
|:-----------:|
|![Alt](images/portada.jpg)|
| INSTALACIÓN, CONFIGURACIÓN Y DOCUMENTACIÓN DEL CLIENTE DE DESARROLLO |


- [CLIENTE DE DESARROLLO](#cliente-de-desarrollo)
  - [Windows 11](#windows-11)
    - [2.1 **Configuración inicial**](#21-configuración-inicial)
    - [2.2 **Navegadores**](#22-navegadores)
    - [2.3 **MobaXterm**](#23-mobaxterm)
      - [Instalación](#instalación)
      - [Crear una sessión SSH](#crear-una-sessión-ssh)
      - [Crear una sessión SFTP](#crear-una-sessión-sftp)
    - [2.4 **Netbeans**](#24-netbeans)
      - [Creación de un proyecto de PHP](#creación-de-un-proyecto-de-php)
      - [Abrir un proyecto de PHP](#abrir-un-proyecto-de-php)
      - [Depurar un fichero en Netbeans](#depurar-un-fichero-en-netbeans)
    - [2.5 **Visual Studio Code**](#25-visual-studio-code)

## Windows 11
### 2.1 **Configuración inicial**
* Despues de instalar el ubuntu server en la maquina virtual se prueba la conexion con el anfitrion.
para ello se abre la terminal de windows

![alt text](images/cmdWindows.png)

* En la terminal de windows se hace ping con la ip de la maquina virtual.
```bash
ping ipDelServidor
```

![alt text](images/cmdPingWindows.png)
Si todos los paquetes se han recibido es que las maquinas están conectadas.

* Nos podemos conectar al servidor desde la terminal de windows con este comando
```bash
ssh usuario@ipServidor
```
Nos pedira la contraseña ya se podrá trabajar en el servidor.

![alt text](images/cmdConServidorAnfitrion.png)

* Para salir del Servidor
* 
![alt text](images/cmdLogoutWindows.png)

### 2.2 **Navegadores**
Se puede utilizar cualquier navegador para visualizar el proyecto que está en el Servidor.
* Para poder visualizar el proyecto, se deberá de indicar la url del proyecto.
* 
  ![alt text](images/navegadorURL.png)


### 2.3 **MobaXterm**
#### Instalación 
Descargar MobaXterm en este enlace : https://mobaxterm.mobatek.net/download.html

#### Crear una sessión SSH
* Para crear una sesión ssh, hacer clic en el botón de session arriba a la izquierda. 

![Alt](images/moba-crearSesion.png)

* Cuando aparezca la ventana, hacer clic en SSH

![Alt](images/moba-crearSesionSsh.png)

* Se rellena. El host, es la IP del servidor y se puede indicar el usuario si se quiere, y se le da a OK
* 
![Alt](images/moba-crearSesionSsh2.png)

* Se hace clic en la conexión, que se encuentra  en la parte izquierda.

![Alt](images/moba-entrarSesionSsh.png)

* Aparece la terminal con el usuario, si se ha indicado en la creación, sino habrá que indicar el usuario y la contraseña.
![Alt](images/moba-entrarSesionSsh2.png)


#### Crear una sessión SFTP
* Para crear una sesión sftp, hacer clic en el botón de session arriba a la izquierda. 

![Alt](images/moba-crearSesion.png)

* Cuando aparezca la ventana, hacer clic en SFTP
![alt text](images/moba-crearSessionSFTP.png)


* Se rellena. El host, es la IP del servidor y se puede indicar el usuario si se quiere, y se le da a OK

![alt text](images/moba-CrearSessionSFTP2.png)

* Nos pide la contraseña
![alt text](images/mobaCrearSessionSFTP3.png)


* Se abre la terminal con el usuario.
![Alt](images/moba-CrearSessionSFTP4.png)



### 2.4 **Netbeans**

#### Creación de un proyecto de PHP
Se hace clic en File -> New Project o se hace clic en el pestaña del cuadrado naranja con un más

![Alt](images/File-NewProject.png)


![Alt](images/botonNewProject.png)

En el primer paso de la creación de proyecto, se selecciona PHP en Categories, y PHP Aplicación from Remote Server y se hace clic en Next

![Alt](images/newFile-paso1.png)

En el paso 2 se indica el nombre del proyecto, y la ubicación en local
y se hace clic en Next

![Alt](images/newFile-paso2.png)


En el paso 3 se indica la IP del servidor...
![Alt](images/newFile-paso3-1.png)

 y se hace clic en Manage...
 para configurar la conexion al servidor remoto, donde se indicará el nombre del servidor, la IP , el puerto, el nombre del usuario con permisos para actuar en las carpetas del proyecto, la contraseña....

![Alt](images/newFile-paso3-conexion.png)

 se hace un test de conexión y saldrá un mensaje de confirmación

 ![Alt](images/mensajeConfirmacion.png)

   hacer clic en Yes,  si el test es ok, hacer clic en OK...(el servidor remoto tiene que estar encendido sino no hace la conexion)

  ![Alt](images/conexionOk.png)

   se cierra la ventana de conexion se indica la ubicación de la carpeta del proyecto en el servidor y se hace clic en Next en la ventana del paso 3.

![Alt](images/newFile-paso3-2.png)

Sale de nuevo el mensaje de Confirmación de conexión y se hace clic en Yes.

![Alt](images/mensajeConfirmacion.png)

Se checkea que la carpeta del proyecto tenga todos los elementos necesarios y se hace clic en finish.

![Alt](images/newFile-paso4.png)

Sale de nuevo el mensaje de Confirmación de conexión y se hace clic en Yes.

![Alt](images/mensajeConfirmacion.png)

El proyecto aparecerá en la parte izquierda del IDE.

![Alt](images/newFile-Fin.png)

#### Abrir un proyecto de PHP
* Se hace clic en el icono de abrir, o en File - Open Project.

![alt text](images/netbeans-AbrirProj.png) ![alt text](images/netbeans-AbrirProj2.png)

* Aparece una ventana con los proyecto y se elije el que se quiera abrir y se hace clic en open Proyect

![alt text](images/netbeans-AbrirProj3.png)

#### Depurar un fichero en Netbeans
Depurar  sirve para identificar y corregir errores en el código, lo que mejora la estabilidad, fiabilidad y rendimiento del software. Permite ejecutar el código paso a paso, inspeccionar variables y comprender el flujo de ejecución para encontrar la causa raíz de los problemas. 

* Despues de haber elegido el fichero y de haber puesto el o los break point en las lineas de codigo deseadas. 
Para poner los break point hay que hacer clic en la parte izquierda del codido, donde aparecen los cuadraditos rosas en la imagen.
  
![alt text](images/netbeansDebug.png)

* Se hace clic en Debug-Debug File

![alt text](images/netbeansDebug1.png)

* Inicia la depuración y se situa el "cursor" de depuración al principio del codigo . Para que pase al primer break point se hace clic en "play".

![alt text](images/netbeansDebug2.png)

* A cada vez que se para en los break points, en la pestaña de variables, se pueden ver el contenido de las variable en ese momento.

![alt text](images/netbeansDebug3.png)

* Para salir del debug se hace clic en "stop".

![alt text](images/netbeansDebug4.png)

### 2.5 **Visual Studio Code**
