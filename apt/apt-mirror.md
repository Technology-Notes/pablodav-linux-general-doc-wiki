
# Apt-mirror

La configuración estándard está en: 
/etc/apt/mirror.list

# (Se agregan también ppas y mirror a otros servidores externos)
Ejemplo: 
```shell
############# config ##################
#
# set base_path    /var/spool/apt-mirror
#
# set mirror_path  $base_path/mirror
# set skel_path    $base_path/skel
# set var_path     $base_path/var
# set cleanscript $var_path/clean.sh
# set defaultarch  <running host architecture>
# set postmirror_script $var_path/postmirror.sh
# set run_postmirror 0
set nthreads     20
set _tilde 0
#
############# end config ##############
 
deb http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu trusty-security main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu trusty-updates main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu trusty-proposed main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe multiverse
 
#deb-src http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse
#deb-src http://archive.ubuntu.com/ubuntu trusty-security main restricted universe multiverse
#deb-src http://archive.ubuntu.com/ubuntu trusty-updates main restricted universe multiverse
#deb-src http://archive.ubuntu.com/ubuntu trusty-proposed main restricted universe multiverse
#deb-src http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe multiverse
```
 
### También se puede especificar la arquitectura: 

```shell
deb [arch=amd64,i386] http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse
 
#PPa from: https://launchpad.net/~hugo-vanduijn/+archive/ubuntu/burp-latest
deb http://ppa.launchpad.net/hugo-vanduijn/burp-latest/ubuntu trusty main
 
 
# Foreman
# http://theforeman.org/manuals/1.7/quickstart_guide.html
deb http://deb.theforeman.org/ trusty 1.7
deb http://deb.theforeman.org/ plugins 1.7
 
# Puppet
# https://puppetlabs.com/
deb http://apt.puppetlabs.com/ trusty main dependencies
 
#clean http://archive.ubuntu.com/ubuntu
clean http://ppa.launchpad.net/hugo-vanduijn/burp-latest/ubuntu
clean http://deb.theforeman.org/
clean http://apt.puppetlabs.com/
```

Como se muestra en el ejemplo arriba, se pueden agregar repos externos y ppas para sincronizar local  y usar "offline" o en red con otras instalaciones.


## Tarea cron para apt-mirror

Esta tarea es estándard, solo se descomenta la línea de cron para tener sincronización diaria: 

```shell
nagiosadmin@l240lnx03:~$ cat /etc/cron.d/apt-mirror
#
# Regular cron jobs for the apt-mirror package
#
0 4     * * *   apt-mirror      /usr/bin/apt-mirror > /var/spool/apt-mirror/var/cron.log
```

## Preparados links simbólicos en servidor web nginx para poder usar los mirrors en otros servidores: 

`sudo ln -s /var/spool/apt-mirror/mirror/ /var/www/html/mirrors`

Si se quiere se puede poner uno para los ppa:
`sudo ln -s /var/spool/apt-mirror/mirror/ppa.launchpad.net/ /var/www/html/ppa`

Verán todos los repositorios sincornizados en: 
/var/spool/apt-mirror/mirror
 
### Permisos: 
sudo chown root:www-data -R /var/spool/apt-mirror/mirror
 
### Keys: 

Algunas llaves se tienen que descargar e instalar offline. 

1. Preparar directorio: 
 * sudo mkdir /var/www/html/keys
 
#### Descarga de llaves: 

```shell
sudo apt-key adv --recv-key --keyserver keyserver.ubuntu.com  [keyhash] 
gpg --export --armor CE49EC21 > /var/www/html/keys/reponame.pub 
```

**Donde CE49EC21 es la [keyhash]**

https://help.ubuntu.com/community/Repositories/Ubuntu

# Uso del repositorio offline: 

Para configurar el repositorio interno, ejecutar las siguientes ordenes en una terminal logueado al servidor con el usuario administrador.
Los repositorios preparados están documentados en: Preparar repositorio offline apt 

sudo su -  (para abrir como root el bash, el - está incluido en el comando)

1. Quitar instalación por defecto: 
sudo mv /etc/apt/sources.list /etc/apt/sources.list.old 
 
2. Crear nuevo archivo principal

Ejemplo indicando que se use solo arquitectura de 64 bit: 

```shell
/etc/apt/sources.list
#
 
# deb cdrom:[Ubuntu-Server 14.04 LTS _Trusty Tahr_ - Release amd64 (20140416.2)]/ trusty main restricted
 
#deb cdrom:[Ubuntu-Server 14.04 LTS _Trusty Tahr_ - Release amd64 (20140416.2)]/ trusty main restricted
 
# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb [arch=amd64] http://servidorrepositorio/ubuntu/ trusty main restricted
#deb-src http://servidorrepositorio/ubuntu/ trusty main restricted
 
## Major bug fix updates produced after the final release of the
## distribution.
deb [arch=amd64] http://servidorrepositorio/ubuntu/ trusty-updates main restricted
#deb-src http://servidorrepositorio/ubuntu/ trusty-updates main restricted
 
## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb [arch=amd64] http://servidorrepositorio/ubuntu/ trusty universe
#deb-src http://servidorrepositorio/ubuntu/ trusty universe
deb [arch=amd64] http://servidorrepositorio/ubuntu/ trusty-updates universe
#deb-src http://servidorrepositorio/ubuntu/ trusty-updates universe
 
## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team, and may not be under a free licence. Please satisfy yourself as to
## your rights to use the software. Also, please note that software in
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb [arch=amd64] http://servidorrepositorio/ubuntu/ trusty multiverse
#deb-src http://servidorrepositorio/ubuntu/ trusty multiverse
deb [arch=amd64] http://servidorrepositorio/ubuntu/ trusty-updates multiverse
#deb-src http://servidorrepositorio/ubuntu/ trusty-updates multiverse
 
## N.B. software from this repository may not have been tested as
## extensively as that contained in the main release, although it includes
## newer versions of some applications which may provide useful features.
## Also, please note that software in backports WILL NOT receive any review
## or updates from the Ubuntu security team.
#deb http://servidorrepositorio/ubuntu/ trusty-backports main restricted universe multiverse
#deb-src http://servidorrepositorio/ubuntu/ trusty-backports main restricted universe multiverse
 
deb [arch=amd64] http://servidorrepositorio/ubuntu trusty-security main restricted
#deb-src http://servidorrepositorio/ubuntu trusty-security main restricted
#deb http://servidorrepositorio/ubuntu trusty-security universe
#deb-src http://servidorrepositorio/ubuntu trusty-security universe
#deb http://servidorrepositorio/ubuntu trusty-security multiverse
#deb-src http://servidorrepositorio/ubuntu trusty-security multiverse
 
## Uncomment the following two lines to add software from Canonical's
## 'partner' repository.
## This software is not part of Ubuntu, but is offered by Canonical and the
## respective vendors as a service to Ubuntu users.
# deb http://archive.canonical.com/ubuntu trusty partner
# deb-src http://archive.canonical.com/ubuntu trusty partner
 
## Uncomment the following two lines to add software from Ubuntu's
## 'extras' repository.
## This software is not part of Ubuntu, but is offered by third-party
## developers who want to ship their latest software.
# deb http://extras.ubuntu.com/ubuntu trusty main
# deb-src http://extras.ubuntu.com/ubuntu trusty main
``` 


Otro ejemplo: Repositorio para burp ppa: 

```shell
/etc/apt/sources.list.d/burp.list
deb [arch=amd64] http://servidorrepositorio/ppa/hugo-vanduijn/burp-latest/ubuntu/ trusty main
```


3. Borrar cache de sources anterior: 

```shell
rm /var/lib/apt/lists/* 
# O probar primero:
apt-get clean all
```

4. Instalar keys offline:

wget -qO - http://servidorrepositorio/keys/reponame.pub | sudo apt-key add -





