Creé un script que en base a un csv (lista separada por comas) que puedo sacar de miradore o de server list, etc. Verifica todo lo que está ahí y verifica si está en nagios, si no está prueba ping por nombre, si no responde el nombre prueba por ip y luego si responde genera la configuración para copiar y pegar en nagios.
 
### Ejemplo:
`~/nagios_import$ ./nagios_import.sh servers.csv > nagiosimport.log`
`ping: unknown host XXXX`
(mensaje si el ping no responde)
 
Es muy bueno porque nos permite mantener sincronizado el inventario con el monitoreo en segundos.
 
Los campos son: `NOMBRE;DESCRIPCION;IP;PADRE;BOCA_SW`
(No utilizar caracteres especiales en los campos)



Borrar el archivo hosts.cfg.

Ejecutar: `./nagios_import.sh <archivos csv >`

Esto va a generar un nuevo archivo hosts.cfg con la configuración para todos los dispositivos que estaban en el CSV y que no existen en la configuración de nagios.

Luego copiar el contenido a /etc/nagios3/conf.d/ con el nombre adecuado.

### Mejoras planificadas a futuro: 
Uso de pynag para manipular la configuración de forma automática (actualizar, remover, agregar, etc). 

Repositorio con script: 
`git clone https://github.com/pablodav/linux-scripts.git `

Script:
https://github.com/pablodav/linux-scripts/tree/master/scripts/nagios_import 




