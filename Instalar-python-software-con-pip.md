Una opción muy usada para instalar python software es usando pip (instalador en línea), este programa permite instalar todo lo que precisa un software python de una forma muy sencilla y normalmente es un método que funciona mejor que instalar a mano o con los paquetes de la distribución. 

Para tener soporte pip hay que instalar el paquete python: sudo apt-get install python-pip 

Luego es normal que un archivo de requerimientos del software tenga toda la info para instalar este, se pueden instalar estos normalmente usando ese archivo con pip install -r requirements.txt (archivo del software)

También recomiendo tener instalado la posibilidad de usar virtual environment de python, lo que nos permite usar un ambiente python virtual para instalar todo lo que precisemos usando un directorio que se usa como ambiente python, esto permite una gran ventaja porque se pueden instalar versiones diferentes de software en ambientes independientes de python.  sudo apt-get install python-virtualenv
Luego crear directorio mkdir directorio
Y usar este: virtualenv directorio (Ya estará usando este directorio para instalar software python)

Otro método para usar pip, es descargar en un equipo y crear un cache: 
SDIST_CACHE=/directorio/destino
pip install --no-install --use-mirrors -I --download=$SDIST_CACHE <package name>

Luego en la máquina que queremos instalar solo copiamos ese directorio y lo usamos, o usamos nfs para montar el directorio. 
pip install --find-links=file://$SDIST_CACHE --no-index --index-url=file:///dev/null <package name> 
