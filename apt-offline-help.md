
# Package management

## Ubuntu/Debian
### apt-offline
[Apt-offline-help] (https://github.com/pablodav/linux-general-doc-wiki/wiki/apt-offline-help)

#Apt-offline. 
La mayoría de distribuciones de Linux actuales tiene una gran dependencia de Internet a la hora de realizar la instalación de aplicaciones. Si se usan distribuciones como Debian o Ubuntu, y un equipo que no tiene acceso a Internet, la instalación de aplicaciones puede llegar a ser un suplicio.
Apt-offline es una aplicación que sirve para instalar aplicaciones sin necesidad de tener una conexión permanente a Internet. Para ello se debe tener acceso a un ordenador que disponga de conexión a Internet, para realizar las descargas y después se trasladarán dichas descargas a los equipos que no tengan red.
Tanto en el equipo que tenga Internet como el que no lo tenga, hay que instalar apt-offline.
En el equipo que tiene Internet, sólo hay que ejecutar:
sudo apt-get install apt-offline

En el equipo que no tiene Internet, podemos instalar desde las fuentes o descargar el paquete desde los repositorios de Ubuntu (packages.ubuntu.com) e instalarlo manualmente.
Imaginemos que se desea instalar el programa “sqliteman”, por poner un ejemplo. En el ordenador sin Internet se deberá escribir:

##En máquina donde se quiere instalar offline generar archivo con lo que se precisa: 
sudo apt-offline set apt.sig --update --upgrade --install-packages sqliteman
Se generará el archivo “apt.sig”. Este archivo se debe copiar al ordenador con conexión a Internet y ejecutar:

##En computadora con acceso a repos (internet): 
sudo apt-offline get apt.sig --threads 5 --bundle offline.zip
Se generará el archivo “offline.zip”. En el proceso de descarga pueden que salgan algunos mensajes en color rojo de conexiones fallidas. En principio no hay que preocuparse mucho por dichos mensajes.
Ahora sólo hay que copiar el archivo “offline.zip” al ordenador sin conexión y ejecutar:

##En la máquina donde se quiere instalar offline, instalar el software:
sudo apt-offline install offline.zip
Finalmente se ejecuta:
sudo apt-get install sqliteman
El programa quedará instalado en la máquina sin conexión a Internet.
