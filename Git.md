# CFGS Desarrollo de Aplicaciones Web

- [3 Git y GitHub](#3-git-y-github)
    - [3.1 **Git**](#3.1-git)
        - [**Descarga e Instalación**](#descarga-e-instalacion)
        - [**Inicialización y Configuración**](#inicializacion-y-configuracion)
    - [3.2 **Git Hub**](#3.2-github)
      

## 3-Git-y-GitHub

### 3.1 **Git**
    Git es un sistema de control de versiones distribuido gratuito y de código abierto que se utiliza para rastrear los cambios en el código fuente durante el desarrollo de las aplicaciones.
#### **Descarga e Instalación**
 
##### 1. Descargar Git

1. Se accede al sitio oficial de Git:
    [https://git-scm.com/downloads](https://git-scm.com/downloads)
2. Se hace clic en **Windows**.
   Se descarga la versión acorde con su equipo. Existe una versión de escritorio y una portable.
    Al pinchar en el enlace de la versión, que se quiera, la descarga comenzará automaticamente.

---

##### 2. Instalar Git

1. Se ejecuta el instalador descargado.
2. Se acepta los términos de licencia y se siguen los pasos recomendados:
    * **Se elije la carpeta de instalación :** se puede dejar la que viene por defecto.
    * **Select Components:** se puede dejar las opciones por defecto.
    * **Start Menu Folder:** se puede dejar lo que viene por defecto.
    * **Editor por defecto:** se selecciona el editor de texto que se prefiera.
    * **Name of the initial branch:** se puede dejar la que viene por defecto o poner el nombre que se quiera.Es la rama que se creara por defecto al iniciar una repositorio nuevo.
    * **PATH environment:** se recomienda seleccionar :
     `Git from the command line and also from 3rd-party software`.
    * **SSH executable:** se puede dejar la que viene por defecto(bundle ssh) para poder utilizar openSSH. .
    * **HTTPS transport backend:** se puede dejar la que viene por defecto para poder utilizar la libreria de windows .
    * El resto de opciones puedes dejarlas por defecto.
3. Se empieza con la instalación haciendo clic en **Instalar**.
4. Finaliza la instalación haciendo clic en **Finish**.

---

##### 3. Verificar la instalación

 Se abre **Símbolo del sistema (CMD)**, **PowerShell**, **GitBash** o la **terminal de VS Code** y se ejecuta:

```bash
git --version
```

Deberías ver algo como:
```
git version 2.47.1.windows.1
```

---
#### **Inicialización y Configuración**

##### 1. Inicialización 
Se abre el editor de texto dentro de la carpeta del proyecto y se inicializa git.
```bash
git init
```

Tambien se puede clonar de un repositorio de github
  ```bash
  git clone <URL>
  ```
##### 2. Nombre y email 
Se debe de configurar git con un nombre y un correo
Estos datos se asocian a los *commits*:

```bash
git config --global user.name "Nombre"
git config --global user.email "email@ejemplo.com"
```



---

##### 3. Configurar el editor de texto (opcional) 


```bash
git config --global core.editor "editorDeTexto"
```

---
##### 4. Verificar la configuración 

```bash
git config --list
```
---


## 3.2  **GitHub**
