 **Project: “Cloud Computing in European schools”**  
<img src="/img/cloud-computing-logoproject.jpg" height="100" width="170"/>

 Number: Project: 2017-1-ES01-KA202-038471

<img src="/img/cofinanciadoEN.png" height="50" width="200"/> <img src="/img/logoIES-Modificado.png" height="75" width="200"/>  




# Introduction to PaaS: develop, deploy, run and manage apps on the Cloud  



#### Disclaimer
&nbsp;&nbsp;&nbsp;  *"The European Commission support for the production of this publication does not constitute an endorsement of the contents which reflects the views only of the authors, and the Commission cannot be held responsible for any use which may be made of the information contained therein."*




#### Author

&nbsp;&nbsp;&nbsp;  This material has been produced by José Luis Rodríguez Rodríguez under the Creative Commons licence:  <img src="/img/Licencia-Tipo2.png" height="25" width="75"/>  




### Objective
&nbsp;&nbsp;&nbsp; Platform as a Service (PaaS), is a cloud computing model that allows the users to develop, deploy, run and manage applications without taking care about the underlying layers. The alternatives used today focus on the use of containers which promote the **microservices based application** development approach (vs **monolithic applications**), because the different services into which we the application is separated can easily run in different containers. We will make a study of Docker, Kubernetes and OpenShift in order to develop, deploy, run and manage  microservices based applications.

&nbsp;&nbsp;&nbsp;This activity has been developed for developing the professional competence includes in the Erasmus+ project "Cloud Computing in European Schools".

</br>
</br>
</br>

![](media/23f9418b60308fd28c9811aa0e6b09bb.jpg)

**By:**

-   Daniel Salud Cornejo

-   Norberto Olivas Alonso

-   David Delgado Pineda

**Profesor:** José Luís Rodriguez Rodriguez

**Líder del equipo:** Norberto Oliva Alonso

*Índice del proyecto*

*1.-Distribución del trabajo*
=============================

-   **Norberto Oliva Alonso.**

    -   Elaboración del trabajo,encargado de subir este a git y elaboración del
        readme

-   **David Delgado Pineda**

    -   Documentación de la segunda parte del proyecto(a partir del 3.10).

-   **Daniel Salud Cornejo.**

    -   Documentación de la primera parte del proyecto(de la parte 3 hasta la
        3.10)

*2.-Introducción*
=================

La idea detrás de Docker es crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues.
=====================================================================================================================================================================================================================================================================================

*3.-Instalación de Docker.*
===========================

**3.1 Instalar vagrant**
------------------------

El primer paso sería la instalación de Vagrant, para ello debemos introducir el
siguiente comando en la consola:

*sudo apt-get install vagrant*

![](media/9680a7f9d23d62c1e03f3133ab210d42.png)

**3.2 Instalar VirtualBox**
---------------------------

Una vez instalado vagrant vamos a descargar VirtualBox, para ello introducimos
este comando en la consola

*sudo-apt-get install virtualbox*

![](media/c3239cea391362b77ad503f43d954b16.png)

**3.3 Crear la carpeta vagrant**
--------------------------------

Continuaremos poniendo en la consola el comando:

*cd \$Home*

Una vez puesto nos llevará al Home donde introduciremos el siguiente comando en
la consola:

*mkdir Vagrant*

Una vez hecho esto ya tendremos creada nuestra carpeta

![](media/87d2fe2dd409acda5829857803389fd8.png)

**3.4 Accedemos a la carpeta vagrant y creamos public_html**
------------------------------------------------------------

Para poder acceder a la carpeta que hemos creado debemos poner el siguiente
comando:

*cd Vagrant*

De esta manera accederemos a la carpeta previamente creada y podremos el
siguiente comando:

*mkdir public_html*

![](media/6f3f6cca46da9c095ddbf589a3d4a07a.png)

**3.5 Accedemos a public_html y creamos el fichero index**
----------------------------------------------------------

Accedemos a public_html con el comando:

*cd public_html*

Una vez aquí introducimos esto:

*echo “\<h1\>Prueba\</h1\>”\> index.html*

![](media/998431870844b4d80114a99d0aecc192.png)

**3.6 Creamos la carpeta MvDocker y accedemos a ella**
------------------------------------------------------

### Para este paso debemos acceder a la carpeta Vagrant poniendo el comando:

*cd ..*

A continuación ponemos este comando en la consola:

*mkdir MvDocker*

Después de esto accederemos a ella con el comando

>   *cd MvDocker*  
>   

![](media/90f078c0d38b36371711b5682b79b6c7.png)

![](media/e6f7a830aa38f68bb85517fb641a9ecf.png)

**3.7Creamos el fichero DockerFile**
------------------------------------

Ponemos el comando:

*nano DockerFile*

Y escribimos en él todo lo que se ve en la imagen de abajo

![](media/40456b8e76fd83dff3039cf76bba6390.png)

**3.8 Descargamos ubuntu**
--------------------------

Introducimos el siguiente comando:

*vagrant box add ubuntu/bionic64*

![](media/37e0a3fd1b4edeba8ddd413cbef8630e.png)

**3.9 Creamos VagrantFile**
---------------------------

Ponemos el comando:

*nano VagrantFile*

Y escribimos en él todo lo que se ve en la imagen de abajo

![](media/6ec33d68fc2b7545414a87cd772deb77.png)

**3.10 Arrancar vagrant**

Ponemos :

*vagrant up*

y en teoria deberia de funcionar, pero hemos probado todas las maneras y no
funciona

![](media/844bec409b68daceaf3d1facea54fa39.png)

**3.10 Después de arrancar vagrant**

Una vez estemos conectados en la máquina virtual, crearemos la página web
index.html en la carpeta public_html. También crearemos el fichero Dockerfile.

Luego crearemos la imagen de Docker con el siguiente comando:

*docker build -t jlr2/aplicacionesweb: v1*

También debemos de crear y ejecutar el contenedor en el entorno de desarrollo
con el comando:

*docker run --name aplweb -d -p 80:80 jlr2/aplicacionesweb: v1*

Para subir la imagen que hemos creado sería con el comando:

*docker push jlr2/aplicacionesweb: v1*

Debemos de desplegar la aplicación en nuestro entorno con:

*docker pull jlr2/aplicacionesweb:v1*

En el caso de que queramos modificar la aplicación, debemos de crear una nueva
imagen:

*docker build -t jlr2 / aplicacionweb: v2*

Luego la tenemos que cargar:

*docker push jlr2/aplicacionesweb: v2*

Seguidamente descargarnos la nueva imagen al entorno:

*docker pull jlr2/aplicacionesweb: v2*

Para eliminar el contenedor actual se usaría el comando:

*docker container rm -f aplweb*

Como hemos hecho antes volvemos a correr el nuevo contenedor:

*docker run --name aplweb2 -d -p 80:80 jlr2/aplicacionesweb:v2*

*4.-Conclusión*
===============

Este proyecto ha sido interesante, ya que hemos aprendido las diferentes
utilidades de docker, cosa que en un futuro trabajo nos puede resultar útil
