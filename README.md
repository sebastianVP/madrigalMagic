#  MADRIGAL Y SIGNAL CHAIN
---
## TUTORIAL PARA INSTALAR Y GENERAR ARCHIVOS EN FORMATO MADRICAL CON SIGNAL CHAIN

1. El objetivo es generar los atributos estandares de Madrigal, con el metodo de escritura desarrollado en Signal Chain.
   Para esto se requiere:

   * Instalar Madrigal.
   * Instalar Signal Chain branch ISR.

2. Definimos para este objetivo una carpeta de trabajo y un entorno de desarrollo desde anaconda.

3. Usaremos la version de python=3.11.

   Con este comando nuestro entorno se llama **madrigal_v**   
   $ conda create --name madrigal_v python=3.11

   Para activarlo escribimos:\
   $ conda activate madrigal_v 

   Creamos la carpeta.\
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

5. Nuestro primer paso  en este punto para instalar la libreria madrigal. Activar el entorno virtual y ubicarse en el siguiente directorio:

   $ conda activate madrigal_v\
   $ cd /home/soporte/workspace/MADRIGAL_MAGIC/MADROOT

   Ahora probamos para verificar que no tenemos instalado madrigal, esto deberia arrojarnos :
   $ python 
   >> import madrigal\
   ModuleNotFoundError: No module named 'madrigal'
   >> exit()
   
   Hemos verificado que no hay una instlacion previa con los comandos anteriores, la forma rapida de instalar los paquete pre-requisitos es utilizar el comando pip.
   Pero debido a una actualizacion debemos modificar un archivo adicional. Dentro de la carpeta MADROOT
   
   $ nano required_modules.txt

   Modificamos la linea 11 y escribimos en lugar de solo **bootstrap3** lo siguiente **django-bootstrap3**

   Cerramos el archivo y el paso siguiente es utilizar el comando pip.

   $ pip install -r required_modules.txt

   La opcion mostrada a continuacion seria una forma de instalar los pre-requisitos paso a paso. **Pero es mejor solo utilizar la secuencia de pasos anteriores** y saltar **al punto 6**.
   En nuestro entorno de desarrollo de manera satisfactoria, para esto se requiere instalar las siguientes librerias.
   ##### OPCIONAL #####   
   $ conda install h5py\
   $ conda install matplotlib\
   $ conda install netCDF4 \
   $ conda install scipy\
   $ conda install django\
   $ conda install django-bootstrap3\
   $ pip install aacgmv2\
   $ pip install filelock\
   $ bash installMadrigal  &> install.log &\
   $ cat install.log\

   Para verificar la correcta instalacion

   $ python
   >> import madrigal

6. Luego instalar de manera correcta Signal Chain, aqui debemos utilizar el branch de ISR desarrollado por Roberto.

   $ git clone http://intranet.igp.gob.pe:8082/schain
   $ cd schain/ \
   $ git init\
   $ git status\
   $ git checkout isr\
   $ cd schainpy
   $ pip install -e ../ \
   $ pip install click\
   $ pip install zmq


