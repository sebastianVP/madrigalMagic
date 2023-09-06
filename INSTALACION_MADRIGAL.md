#  MADRIGAL Y SIGNAL CHAIN
---
## TUTORIAL PARA INSTALAR Y GENERAR ARCHIVOS EN FORMATO MADRIGAL CON SIGNAL CHAIN

RECOMENDACIONES PREVIAS de COMPILADORES:

* Instalar paquetes de C y fortran.
  
  $ sudo apt install -y --no-install-recommends gcc gfortran build-essential automake autotools-dev autoconf m4 libtool hdf5-tools libhdf5-dev libnetcdf-dev pkg-config\
  $ sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev libgdbm-dev libnss3-dev libedit-dev libc6-dev\
  $ sudo apt-get -yq install build-essential gdb lcov libbz2-dev libffi-dev libgdbm-dev  liblzma-dev libncurses5-dev libreadline6-dev libsqlite3-dev libssl-dev lzma lzma-dev  tk-dev uuid-dev xvfb zlib1g-dev


  Verificar con el comando

  $ dpkg -L gcc

**NOTA:** 

1. Se recomienda tener instalado por defecto  gfortran-9, para verificar en consola escribir:

   $ gfortran --version

2. La PC de operaciones es un S.O. ubuntu 22.04, aqui logre instalar Madrigal  con los siguientes paquetes.:

 
   *  automake 1.16.1
   *  autoconf 2.69
   *  gfortran 9.4.0
   *  libtoolize 2.4.6

#### LINK ####
Este link puede servir de tutorial solo en caso no se tengan los compiladores 

[tutorial](https://techglimpse.com/install-update-autoconf-linux-tutorial)
 

# INSTALACION

1. El objetivo es generar los atributos estandares de Madrigal, con el metodo de escritura desarrollado en Signal Chain.
   Para esto se requiere:

   * Instalar Madrigal.
   * Instalar Signal Chain branch ISR.

2. Definimos para este objetivo una carpeta de trabajo y un entorno de desarrollo desde anaconda.

3. Usaremos la version de python=3.6.
   
   Debemos tener instalado previamente anaconda o miniconda3  para continuar con la ejecucion de comandos.

   Con este comando nuestro entorno se llama **mad_test**   
   $ conda create --name mad_test python=3.6

   Para activarlo escribimos:\
   $ conda activate mad_test

   Creamos la carpeta llamada DIR_MADRIGAL.\
   $ cd /home/operaciones\
   $ mkdir DIR_MADRIGAL\
   $ cd /home/operaciones/DIR_MADRIGAL\

   Nota: Se puede crear la carpeta con el nombre que se desea, solo respetar luego el orden de los directorios.

4. Descargamos dentro de la carpeta DIR_MADRIGAL el siguiente archivo desde el link:
   
   [Madrigal_Modificado](https://drive.google.com/file/d/1Kjt5LUQBGwLXx3h7eH7fKRX8fW9pfuz6/view?usp=drive_link)

   El archivo se llama **MADROOT.tar.xz**.

   Aqui se incluyen 2 directorios: 
   * **Download Madrigal 3.2.7**
   * **Download Madrigal 3 Sample Experiments (needed when Madrigal first installed)**
   Hemos modificado los archivos de configuracion para que la instalacion sea mas practica, pero debemos todavia modificar algunos archivos.

   Copiamos y descomprimimos en la carpeta indicada /home/operaciones/DIR_MADRIGAL el archivo con extension tar.xz, el directorio se llama MADROOT

   $ cd /home/operaciones/DIR_MADRIGAL

   $ tar -zxf MADROOT.tar.xz
   
   $ cd /home/operaciones/DIR_MADRIGAL/MADRROOT 

   Antes de  la instalacion de librerias prerequisitos de python para utilizar correctamente Madrigal se requiere 3 pasos:
    * Vincular el comando python(4.1 Referencia)
    * Modificar el archivo madrigal.cfg(4.2)
    * Modificar los archivos isrim.f,irifun.f,irisub.f del directorio /home/operaciones/DIR_MADRIGAL/MADROOT/source/madf/geolib y cedar.h del directorio /home/operaciones/DIR_MADRIGAL/MADROOT/source/madc/include(4.3).

### 4.1. Referencia de python de MADROOT, para esto nos ubicamos en el siguiente directorio.

    $ cd /home/operaciones/DIR_MADRIGAL/MADROOT/bin
   
    Escribimos aqui el siguiente comando:

    $ ln -s /home/operaciones/miniconda3/envs/mad_test/bin/python python 

### 4.2 Modificar  el archivo madrigal.cfg

    Nos ubicamos en el directorio siguiente: 
    $ cd /home/operaciones/DIR_MADRIGAL/MADROOT/ 

    Modificamos el archivo  
    $ nano madrigal.cfg 
    Cambios en la linea 9:
    
    MADROOT = /home/operaciones/DIR_MADRIGAL/MADROOT
        
### 4.3 Modificar los archivos con extension .f y h. 
 
    Directorio de archivos fortran.

    $ cd /home/operaciones/DIR_MADRIGAL/MADROOT/source/madf/geolib

    Editamos el archivo isrim.f

    $ nano isrim.f\
    Modificamos la linea 184 que inicia con MADDIR..., aqui escribimos nuestra ruta de directorio de instalacion:\
    MADDIR = '/home/operaciones/DIR_MADRIGAL/MADROOT'

    $ nano irifun.f\
    Modificamos la linea 5930 que inicia con MADDIR..., aqui escribimos nuestra ruta de directorio de instalacion:\
    MADDIR = '/home/operaciones/DIR_MADRIGAL/MADROOT'  

    $ nano irisub.f\
    Modificamos la linea 309 que inicia con MADDIR..., aqui escribimos nuestra ruta de directorio de instalacion:\
    MADDIR = '/home/operaciones/DIR_MADRIGAL/MADROOT'

    Directorio de archivos .h
 
    $ cd /home/operaciones/DIR_MADRIGAL/MADROOT/source/madc/include\
    $nano cedar.h\
    Modificamos la linea 11 , aqui escribimos nuestra ruta de directorio de instalacion:\
    #define __MAD_ROOT__ "/home/operaciones/DIR_MADRIGAL/MADROOT"

5. Para instalar la libreria madrigal debemos activar el entorno virtual y ubicarse en el siguiente directorio:

   $ conda activate mad_test\
   $ cd /home/operaciones/DIR_MADRIGAL/MADROOT

   Ahora probamos el siguiente comando para verificar que no tenemos instalado madrigal, esto deberia arrojarnos :
   $ python 
   >> import madrigal\
   ModuleNotFoundError: No module named 'madrigal'
   >> exit()
   
   Hemos verificado que no hay una instalacion previa con los comandos anteriores.

   La opcion mostrada a continuacion seria una forma de instalar los pre-requisitos paso a paso en nuestro entorno de desarrollo de manera satisfactoria con el comando conda, para esto se requiere instalar las siguientes librerias.
 
    $ python testRequirements.py\ 
    $ pip instal numpy==1.19.5\
    $ pip instal h5py==2.10.0\
    $ pip install matplotlib==3.3.4\
    $ pip install netCDF4==1.5.8\ 
    $ pip install scipy==1.5.3\ 
    $ pip install django==3.2.10\
    $ pip install django-bootstrap3\
    $ pip install aacgmv2==2.6.2\
    $ python testRequirements.py\ 

   # **ATENCION - PASO IMPORTANTE**

       Ubicarse en el directorio MADROOT, para esto debemos tener el entorno activado, en caso no tengamos el entorno activado en la consola, el comando previo es:

       $ conda activate mad_test
   
       $ cd /home/operaciones/DIR_MADRIGAL/MADROOT
    
       Ejecutar el comando de verificacion de paquetes python instalados.

       $ python testRequirements.py
  
       Debemos leer con atencion que paquete esta faltando o si aparece el mensaje de que todos los modulos han sido correctamente instalados. Si y solo si aparece el  siguiente mensaje  podemos continuar con la instalacion.
   
       **All required python modules found.**
   
       Si obtenemos el mensaje en negrita podemos proceder con la instalacion.

       Al ejecutar estos comandos se generar los archivos c, fortran  y sus ejecutables. Existe un posible error adicional que se pueda generar en caso falle la generacion  de estos archivos y esta relacionado a la version de fortran, por ello se recomienda utilizar fotran-9, autoconf-2.69.

       Despues de la verificacion, instalamos con el siguiente comando **Madrigal**:

   # **PASO DE INSTALACION DE COMANDO**

       $ bash installMadrigal  &> install.log &
       Para visualizar toda la instalacion en consola  se recomienda solo

       $ bash installMadrigal

       $ cat install.log

   
       Si todo es correcto , las ultimas lineas muestran el mensaje:

       /home/operaciones/DIR_MADRIGAL/MADROOT/bin/python /home/operaciones/DIR_MADRIGAL/MADROOT/source/madpy/scripts/bin/testWebConfig.py

       and verify you get a message that indicates success.


       Elapsed time: 0:13:17\
       Madrigal installation complete
  
       Para verificar la correcta instalacion

       $ python
       >> import madrigal


6. Luego debemos  instalar Signal Chain, aqui debemos utilizar el branch de ISR desarrollado por Roberto. Este branch es el que actualmente permite a Signal Chain escribir datos en formato Madrigal.
   (LAST UPDATE :D )


   $ cd /home/operaciones/DIR_MADRIGAL\
   $ git clone http://intranet.igp.gob.pe:8082/schain

   $ cd schain\
   $ git init\
   $ git status\
   $ git checkout isr\
   $ cd schainpy
   $ pip install -e ../ \
   $ pip install click\
   $ pip install zmq



