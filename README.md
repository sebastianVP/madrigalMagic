#  MADRIGAL Y SIGNAL CHAIN
---
## TUTORIAL PARA INSTALAR Y GENERAR ARCHIVOS EN FORMATO MADRIGAL CON SIGNAL CHAIN

RECOMENDACIONES PREVIAS de COMPILADORES:

* Instalar paquetes de C y fortran.
  
  $ sudo apt-get install gfortran-9\
  $ sudo apt-get install build-essentail\
  $ sudo apt-get install gcc

  Verificar con el comando

  $ dpkg -L gcc

* Instalar autotools
  
  $ sudo apt-get install autotools-dev\
  $ sudo apt-get install autoconf
  
  Verificar con el comando
 
  $ dpkg -L autoconf\

**NOTA:** 
1. Se recomienda tener instalado por defecto  gfortran-9, para verificar en consola escribir:

   $ gfortran --version

2. Mi PC es un S.O. ubuntu 20, aqui logre instalar Madrigal  con los siguientes paquetes.:


*  automake 1.16.1
*  autoconf 2.69
*  gfortran 9.4.0
*  libtoolize 2.4.6

#### LINK ####
  Este link puede servir de tutorial solo en caso no se tengan los compiladores [tutorial](https://techglimpse.com/install-update-autoconf-linux-tutorial/)
 

# INSTALACION

1. El objetivo es generar los atributos estandares de Madrigal, con el metodo de escritura desarrollado en Signal Chain.
   Para esto se requiere:

   * Instalar Madrigal.
   * Instalar Signal Chain branch ISR.

2. Definimos para este objetivo una carpeta de trabajo y un entorno de desarrollo desde anaconda.

3. Usaremos la version de python=3.11.
   
   Debemos tener instalado previamente anaconda para continuar con la ejecucion de comandos.

   Con este comando nuestro entorno se llama **madrigal_v**   
   $ conda create --name madrigal_v python=3.11

   Para activarlo escribimos:\
   $ conda activate madrigal_v 

   Creamos la carpeta workspace y dentro de esta carpeta creamos una carpeta llamada MADRIGAL_MAGIC.\
   $ cd /home/soporte\
   $ mkdir workspace\
   $ cd /home/soporte/workspace\
   $ mkdir MADRIGAL_MAGIC\
   Nota: Se puede crear la carpeta con el nombre que se desea, solo respetar luego el orden de los directorios.

4. Descargamos dentro de la carpeta MADRIGAL_MAGIC  el siguiente archivo desde el link:
   
   http://cedar.openmadrigal.org/madrigalDownload
   
   Aqui descargamos 2 archivos: 
   * **Download Madrigal 3.2.7**
   * **Download Madrigal 3 Sample Experiments (needed when Madrigal first installed)**

   Copiamos y descomprimimos en la carpeta indicada  el primer archivo con extension tar.gz, despues de descomprimir le cambiamos de nombre a la carpeta.
   La carpeta descomprimida originalmente se llama madrigal327 nosotros la llamamos MADROOT
   
   $ cd /home/soporte/workspace/MADRIGAL_MAGIC 

   $ mv madrigal327 MADROOT

   $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT
   
   Antes de  la instalacion de librerias prerequisitos de python para utilizar correctamente Madrigal se requiere 3 pasos:
    * Vincular el comando python(4.1 Referencia)
    * Modificar el archivo madrigal.cfg(4.2)
    * Modificar el archivo siteTab.txt(4.3)

### 4.1. Referencia de python de MADROOT, para esto nos ubicamos en el siguiente directorio.

   $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT/bin
   
   Escribimos aqui el siguiente comando:

   $ln -s /home/soporte/anaconda3/envs/madrigal_v/bin/python python 

### 4.2 Generar el archivo madrigal.cfg

    Nos ubicamos en el directorio siguiente: 
    $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT/ 

    Copiamos el contenido en un nuevo archivo llamado madrigal.cfg y hacemos los siguientes cambios 
    $ cp madrigal.cfg.template  madrigal.cfg 

    Modificamos el archivo  
    $ nano madrigal.cfg 
    Cambios: 
    
    MADROOT = /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT
    MADSERVER = jro.igp.gob.pe
    MADSERVERROOT = MADROOT
    SITEID = 36
    HTMLSTYLE = <BODY BGCOLOR=#FFFFFF LINK=#008000 VLINK=#003366>
    INDEXHEAD = Welcome to the Madrigal Database <BR> at Jicamarca
    ```
    CONTACT = <A HREF="MAILTO:madrigal@jro.igp.gob.pe">Madrigal administator</A><BR>
    ```
    MAILSERVER = localhost
    ```
    #PLOTBUTTONLABEL = Plots/Docs
    ```
### 4.3 Generar el archivo siteTab.txt
    
    Nos ubicamos en el directorio metadata
    $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT/metadata 
    $ cp siteTab.txt.original siteTab.txt 
    
    Editamos el archivo y añadimos lo siguiente al final desde el 36
    $ nano siteTab.txt 
    
    36,JRO,jro-db.igp.gob.pe,madrigal,cgi-bin/madrigal,/madrigal/servlets,Marco Milla,Jicamarca Radio Observatory,Jicamarca,,,Lima,,Peru,511 317 2313,juan.espinoza@jro.igp.gob.pe,3.0
   
    Despues de añadir esta linea y guardar ya se puede proceder a instalar las librerias.

### 4.4 Descomprimir experiments.
    Descomprimir la carpeta experiments.tar.gz  dentro de la Carpeta MADROOT, este es el archivo que descargamos en el paso 4 Sample Experiments.


5. Nuestro primer paso  en este punto para instalar la libreria madrigal. Activar el entorno virtual y ubicarse en el siguiente directorio:

   $ conda activate madrigal_v\
   $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT

   Ahora probamos para verificar que no tenemos instalado madrigal, esto deberia arrojarnos :
   $ python 
   >> import madrigal\
   ModuleNotFoundError: No module named 'madrigal'
   >> exit()
   
   Hemos verificado que no hay una instalacion previa con los comandos anteriores.




   La opcion mostrada a continuacion seria una forma de instalar los pre-requisitos paso a paso en nuestro entorno de desarrollo de manera satisfactoria con el comando conda, para esto se requiere instalar las siguientes librerias.
 
   $ conda install h5py\
   $ conda install matplotlib\
   $ conda install netCDF4 \
   $ conda install scipy\
   $ conda install django\
   $ conda install django-bootstrap3\
   $ pip install aacgmv2\
   $ pip install filelock\

   # **ATENCION - PASO IMPORTANTE**

   Ubicarse en el directorio MADROOT, para esto debemos tener el entorno activado, en caso no tengamos el entorno activado en la consola, el comando previo es:

   $ conda activate madrigal_v
   
   $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT
    
   Ejecutar el comando de verificacion de paquetes python instalados.

   $ python testRequirements.py
  
   Debemos leer con atencion que paquete esta faltando o si aparece el mensaje de que todos los modulos han sido correctamente instalados. Si y solo si aparece el  siguiente mensaje  podemos continuar con la instalacion.
   
   **All required python modules found.**
   
   Si obtenemos el mensaje en negrita podemos proceder con la instalacion.

   Al ejecutar estos comandos se generar los archivos c, fortran  y sus ejecutables. Existe un posible error adicional que se pueda generar en caso falle la generacion  de estos archivos y esta relacionado a la version de fortran, por ello se recomienda utilizar fotran-9, autoconf-2.69.Verificar las versiones en caso error. La explicacion a detalle se mostrara en el  ANEXO FINAL.

   Despues de la verificacion, instalamos con el siguiente comando **Madrigal**:

   # **PASO DE INSTALACION DE COMANDO**

   $ bash installMadrigal  &> install.log &

   $ cat install.log

   
   Si todo es correcto , las ultimas lineas muestran el mensaje:

   checking that generated files are newer than configure... done\
   configure: creating ./config.status\
   config.status: creating Makefile\
   config.status: creating madf/geolib/Makefile\
   config.status: creating madf/applications/Makefile\
   config.status: creating madc/madrec/Makefile\
   config.status: creating config.h\
   config.status: executing depfiles commands\

  Para verificar la correcta instalacion

    $ python
    >> import madrigal


6. Luego debemos  instalar Signal Chain, aqui debemos utilizar el branch de ISR desarrollado por Roberto. Este branch es el que actualmente permite a Signal Chain escribir datos en formato Madrigal.
   (LAST UPDATE :D )

   $ git clone http://intranet.igp.gob.pe:8082/schain

   $ cd schain\
   $ git init\
   $ git status\
   $ git checkout isr\
   $ cd schainpy
   $ pip install -e ../ \
   $ pip install click\
   $ pip install zmq


### ANEXO FINAL ###

Un posible de error en la instalacion nos puede ocasionar el error de visualiar 2 veces el directorio de instalacion MADROOT en  los ejecutables con extension .f que empiezan con la letra i y que estan ubicados en el directorio.

/home/soporte/workspace/MADRIGAL_MAGIC/MADROOT/source/madf/geolib , osea en ../source/madf/geolib, cuando ocurre esto lo mas recomendable es borrar todos los archivos que empiezan con la letra i dentro de esta  carpeta y desde un directorio con un archivo de instalacion nuevo, descomprimirlo desde la misma ruta copiar los archivos de las mismas caracteristicas es decir que empiezan con letra i y tiene extension .f.

En comando esto seria algo asi:

$ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT/source/madf/geolib
$ rm -r i*

y Desde una carpeta con el archivo madrigal327 descomprimida copiar los archivos y reponerlos en el directorio anterior. En mi caso esta ubicado y descomprimido en Downloads.

$  /home/soporte/Downloads/madrigal327/source/madf/geolib
$ cp i*  /home/soporte/Downloads/madrigal327/source/madf/geolib

y ubicarse nuevamente en el directorio

$  cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT

y volver al **PASO DE INSTALACION DE COMANDO**  MADRIGAL


