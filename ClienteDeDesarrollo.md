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
      - [Instalación y Configuración de phpDocumentor en Windows con NetBeans](#instalación-y-configuración-de-phpdocumentor-en-windows-con-netbeans)
      - [Requisitos Mínimos](#requisitos-mínimos)
      - [1. Instalación de PHP en Windows](#1-instalación-de-php-en-windows)
      - [2. Descargar phpDocumentor](#2-descargar-phpdocumentor)
      - [3. Configuración de NetBeans](#3-configuración-de-netbeans)
      - [4. Generar Documentación desde NetBeans](#4-generar-documentación-desde-netbeans)
  - [](#)
      - [5. Solución de Problemas](#5-solución-de-problemas)
      - [Uso de Git con Netbeans](#uso-de-git-con-netbeans)
    - [2.5 **Visual Studio Code**](#25-visual-studio-code)
      - [Uso de Git con Visual](#uso-de-git-con-visual)
      - [Instalación y Configuración de phpDocumentor en Windows](#instalación-y-configuración-de-phpdocumentor-en-windows)
      - [Requisitos Mínimos](#requisitos-mínimos-1)
      - [Instalación de PHP en Windows](#instalación-de-php-en-windows)
      - [Ejecutar phpDocumentor en Visual](#ejecutar-phpdocumentor-en-visual)
    - [2.6 **Complementos de phpDocumentor**](#26-complementos-de-phpdocumentor)
      - [Instalación de Graphviz](#instalación-de-graphviz)
      - [Alternativa: Doxygen](#alternativa-doxygen)


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


#### Instalación y Configuración de phpDocumentor en Windows con NetBeans

#### Requisitos Mínimos

- **Sistema Operativo**: Windows 10 o superior
- **PHP**: Versión 8.1 o superior (en este manual se usa PHP 8.3.29)
- **NetBeans IDE**: Versión 12 o superior
- **Extensiones PHP requeridas**:
  - php-xml (DOM, XMLWriter, SimpleXML)
  - php-mbstring
- **Espacio en disco**: Al menos 100 MB para PHP y phpDocumentor
- **Opcional**: Graphviz (para generar diagramas de clases)

---

#### 1. Instalación de PHP en Windows

- **Descargar PHP**

1. Ir la página oficial: [https://windows.php.net/download/](https://windows.php.net/download/)
2. Descargar la versión **Thread Safe** (TS) en formato ZIP
   ![alt text](images/ClienteDeDesarrollo/image-2.png)
3. Extraer el contenido en una carpeta.

 - **Configurar Variables de Entorno**

1. Abrir **Variables de entorno del sistema**:
   - Clic derecho en "Este equipo" → Propiedades → Configuración avanzada del sistema → Variables de entorno
2. En **Variables del sistema**, buscar la variable `Path` y hacer clic en **Editar**
3. Añadir la ruta donde se encuentra `php.exe`:
![alt text](images/ClienteDeDesarrollo/image.png)
4. Aceptar y cerrar

 - Verificar la instalación de PHP

Abrir una terminal (CMD o PowerShell) y ejecutar:
```cmd
php -v
```  

![alt text](images/ClienteDeDesarrollo/image-1.png)  

---

#### 2. Descargar phpDocumentor

1. Visitar la página oficial: [https://docs.phpdoc.org/guide/getting-started/installing.html](https://docs.phpdoc.org/guide/getting-started/installing.html)
2. Descargar el archivo **phpDocumentor.phar**:
```
   https://phpdoc.org/phpDocumentor.phar
```  
![alt text](images/ClienteDeDesarrollo/image-3.png)  
3. Guardar el archivo en una ubicación accesible:
```
   D:\Software\phpdoc\phpDocumentor.phar
```

---

#### 3. Configuración de NetBeans

- **Configurar PHP en NetBeans**

1. Abrir NetBeans
2. Ir a **Tools** (Herramientas) → **Options** (Opciones)
3. Seleccionar la pestaña **PHP**
4. En **PHP**, hacer clic en **Browse** y seleccionar la ubicación del ejecutable de PHP:
```
   D:\Software\phpdoc\php-8.3.29\php-8.3.29-Win32-vs16-x64\php.exe
```  
![alt text](images/ClienteDeDesarrollo/image-4.png)  

5. Aplicar los cambios

- **Configurar phpDocumentor en NetBeans**

1. En **Options** → **PHP** → **Frameworks & Tools**
2. Seleccionar la pestaña **PHPDoc**
3. Hacer clic en **Browse** y seleccionar la ubicación de `phpDocumentor.phar`:
```
   D:\Software\phpdoc\phpDocumentor.phar
```
4. Aplicar y aceptar

---

#### 4. Generar Documentación desde NetBeans

- **Abrir el Proyecto**

1. Abrir el proyecto PHP en NetBeans
2. Ejemplo: `D:\ProyectosNetbeans\DAW2LibreriaValidacion`

- **Ejecutar phpDocumentor**

**Opción 1: Desde el menú de NetBeans**
1. Clic derecho sobre el proyecto
2. Seleccionar **Generate Documentation** (Generar documentación)

Para que no salga el error, ir a **Properties** - **Documentación** e indicar la carpeta Target
![alt text](images/ClienteDeDesarrollo/image-5.png)

**Opción 2: Desde la línea de comandos**

1. Copiar el comando generado por NetBeans (aparece en la ventana de salida)
2. Ejecutar en CMD:
```cmd
"D:\Software\phpdoc\php-8.3.29\php-8.3.29-Win32-vs16-x64\php.exe" "D:\Software\phpdoc\phpDocumentor.phar" "run" "--ansi" "--directory" "D:/ProyectosNetbeans/DAW2LibreriaValidacion" "--target" "D:/ProyectosNetbeans/DAW2LibreriaValidacion/doc" "--title" "DAW2LibreriaValidacion"
```
![alt text](images/ClienteDeDesarrollo/image-6.png)
---

#### 5. Solución de Problemas

Si aparece un error relacionado con espacios o rutas en `Program Files\`, la solución es:

1. Crear una carpeta `.phpdoc` en la raíz del proyecto
2. Crear un archivo de configuración XML (`phpdoc.xml`) dentro de `.phpdoc`

3. Ejecutar nuevamente el comando

---

#### Uso de Git con Netbeans
- **Inicializar un proyecto en git**
Estando selecionado el proyecto:
Teams - Git - Initialize Repository  
![alt text](images/ClienteDeDesarrollo/image-17.png)  

o tambien se puede hacer desde el proyecto
Botón derecho - Versionnig - Initialize Git Repository  
![alt text](images/ClienteDeDesarrollo/image-18.png)

Se selecciona la carpeta del proyecto y OK  
 ![alt text](images/ClienteDeDesarrollo/image-19.png)

- **Hacer un commit**
* Primero se añade lo que hay que commitear
Team - Add  
![alt text](images/ClienteDeDesarrollo/image-22.png)
o botón derecho en el proyecto - Git - Add  
![alt text](images/ClienteDeDesarrollo/image-23.png)

* Se hace el commit
Team - Commit   
![alt text](images/ClienteDeDesarrollo/image-20.png)  
o en botón derecho en el proyecto - Git - Commit  
![alt text](images/ClienteDeDesarrollo/image-21.png)  
Se escribe el mensaje del commit, se comprueban los fichero que se han añadido
![alt text](images/ClienteDeDesarrollo/image-24.png)

- **Ver los Commit**
Team - Show History  
![alt text](images/ClienteDeDesarrollo/image-25.png)  
o botón derecho - Git - Show History  
![alt text](images/ClienteDeDesarrollo/image-26.png)  
Se ve el listado de commit  
![alt text](images/ClienteDeDesarrollo/image-27.png)  

- **Crear una rama nueva**
Team - Branch/Tag - Create Branch
![alt text](images/ClienteDeDesarrollo/image-29.png)
o botón derecho en el proyecto - Git - Branch/Tag - Create Branch    
![alt text](images/ClienteDeDesarrollo/image-28.png) 

Se indica el nombre de la rama y se puede elegir que se cambie de rama al crearla o no   
![alt text](images/ClienteDeDesarrollo/image-30.png)  
En este caso se cambiará de rama

- **Cambiar de rama**
Botón derecho - Git - Branch/Tag - Switch To Branch...
![alt text](images/ClienteDeDesarrollo/image-31.png)  
Se elige la rama y OK   
![alt text](images/ClienteDeDesarrollo/image-32.png)

- **Abrir el navegador de repositorios**
Botón derecho - Git - Repository - Repository Browser  
![alt text](images/ClienteDeDesarrollo/image-33.png)  
Se ve el navegador  
![alt text](images/ClienteDeDesarrollo/image-34.png)  

### 2.5 **Visual Studio Code**

#### Uso de Git con Visual  
- **Inicializar un repositorio**  
Icono de Git en la parte izquierda - Initialize Repository  
![alt text](images/ClienteDeDesarrollo/image-35.png)

- **Hacer un commit**
Icono de Git en la parte izquierda, en la pantalla de Git, se hace clic en los 3 puntitos en la linea de CHANGES
changes - Stages All changes(si se quieren pasar todos los cambios)  
![alt text](images/ClienteDeDesarrollo/image-36.png)
Sino se pasan los archivos que se quieran con el + que se encuentra al lado del nombre del archivo   
![alt text](images/ClienteDeDesarrollo/image-37.png)
Se escribe el mensaje de Commit y se hace clic en commit  
![alt text](images/ClienteDeDesarrollo/image-38.png)  

- **Crear Una rama**
Los tres puntitos de CHANGES - Branch - Create Branch  
![alt text](images/ClienteDeDesarrollo/image-39.png)  
Aparece un cuadro de texto para indicar el nombre de la rama  y enter
![alt text](images/ClienteDeDesarrollo/image-40.png)  
Se cambia automaticamente y se puede ver el nombre de la rama en la que estamos abajo a la izquierda  
![alt text](images/ClienteDeDesarrollo/image-41.png)  

- **Cambiar de Rama**
Hacer clic en el nombre de la rama y aparece un menu  y se elige la rama a la que se quiere ir
![alt text](images/ClienteDeDesarrollo/image-42.png)

#### Instalación y Configuración de phpDocumentor en Windows

#### Requisitos Mínimos

- **Sistema Operativo**: Windows 10 o superior
- **PHP**: Versión 8.1 o superior (en este manual se usa PHP 8.3.29)
- **NetBeans IDE**: Versión 12 o superior
- **Extensiones PHP requeridas**:
  - php-xml (DOM, XMLWriter, SimpleXML)
  - php-mbstring
- **Espacio en disco**: Al menos 100 MB para PHP y phpDocumentor
- **Opcional**: Graphviz (para generar diagramas de clases)

---

#### Instalación de PHP en Windows

- Descargar PHP

1. Ir la página oficial: [https://windows.php.net/download/](https://windows.php.net/download/)  
2. Descargar la versión **Thread Safe** (TS) en formato ZIP  
   ![alt text](images/ClienteDeDesarrollo/image-2.png)  
3. Extraer el contenido en una carpeta.

 - Configurar Variables de Entorno

1. Abrir **Variables de entorno del sistema**:
   - Clic derecho en "Este equipo" → Propiedades → Configuración avanzada del sistema → Variables de entorno
2. En **Variables del sistema**, buscar la variable `Path` y hacer clic en **Editar**
3. Añadir la ruta donde se encuentra `php.exe`:  
![alt text](images/ClienteDeDesarrollo/image.png)  
4. Aceptar y cerrar

 - Verificar la instalación de PHP

Abrir una terminal (CMD o PowerShell) y ejecutar:
```cmd
php -v
```  

![alt text](images/ClienteDeDesarrollo/image-1.png)  

---
#### Ejecutar phpDocumentor en Visual
1. Abrir la terminal integrada en VS Code
2. Navegar a la carpeta del proyecto
3. Ejecutar el comando:
```cmd
php D:\Software\phpdoc\phpDocumentor.phar run -d . -t .\doc
```

Donde:
- `-d .`: Directorio actual (código fuente)
- `-t .\doc`: Carpeta de destino para la documentación

---


### 2.6 **Complementos de phpDocumentor**
#### Instalación de Graphviz

Graphviz permite generar diagramas de clases y relaciones entre componentes.

- **Descargar e Instalar**

1. Visitar: [https://graphviz.org/](https://graphviz.org/)
2. Descargar el instalador para Windows
![alt text](images/ClienteDeDesarrollo/image-7.png)

- **Configurar Variables de Entorno**

1. Añadir a la variables de entornos `Path` la ruta de los binarios de Graphviz:  
![alt text](images/ClienteDeDesarrollo/image-8.png)
2. **Importante**: Cerrar sesión y volver a iniciar para que los cambios surtan efecto  

- **Verificar la instalación**
```cmd
dot -v
```  

![alt text](images/ClienteDeDesarrollo/image-9.png)

---

#### Alternativa: Doxygen

Otra herramienta popular para documentación es Doxygen:

- **Sitio web**: [https://www.doxygen.nl/](https://www.doxygen.nl/)
- **Ventajas**: Soporte para múltiples lenguajes (C++, Java, Python, PHP, etc.)
- **Instalación de Doxygen**: 
![alt text](images/ClienteDeDesarrollo/image-10.png)  
![alt text](images/ClienteDeDesarrollo/image-11.png)  
![alt text](images/ClienteDeDesarrollo/image-12.png)  
![alt text](images/ClienteDeDesarrollo/image-13.png)  
![alt text](images/ClienteDeDesarrollo/image-14.png)  
![alt text](images/ClienteDeDesarrollo/image-15.png)  
![alt text](images/ClienteDeDesarrollo/image-16.png)  

---

