Start
===== 

https://www.vagrantup.com/docs/getting-started/ 

Download a vagrant box 
----------------------

It will be used later for your systems, I see it like a template for new vms. 

    vagrant box add centos/7

You can check for more on [vagrant hashicorp catalog](https://atlas.hashicorp.com/boxes/search)

Use http_proxy
-------------

### Linux: 

    export http_proxy='http://user:pass@server:port'
    export https_proxy='http://user:pass@server:port'

### Windows: 

##### CMD

    set http_proxy=http://user:pass@server:port
    set https_proxy=http://user:pass@server:port

##### Powershell (not tested)

    $http_proxy='http://user:pass@server:port'
    $https_proxy='http://user:pass@server:port'
    
---


Create a new folder to start a vm
---------------------------------

    mkdir mynewsystem1 # Create a folder to start
    cd mynewsystem1 

Now initialize as [vagrant project](https://www.vagrantup.com/docs/getting-started/project_setup.html)
----------------------------------

### Use directly to box desired:

    vagrant init centos/7

### Init the vm on the folder without defining a box
    
    vagrant init

Edit the Vagrantfile and put the name of the box you are going to use like: 

    config.vm.box = "centos/7"

### Or just copy an existing folder with Vagrantfile and rename the folder. 
    

Start your vm
-------------
 
    vagrant up

Now access it: 

    vagrant ssh

For More setting follow up: 

https://www.vagrantup.com/docs/vagrantfile/

---


Start with virtualbox
====================

    vagrant up --provider=virtualbox
    

Add virtualbox provider (used for this test)
-------------------------------------------

### Fedora 23 

    sudo dnf install VirtualBox dkms kernel-devel

[Build kernel modules](https://www.if-not-true-then-false.com/2010/install-virtualbox-with-yum-on-fedora-centos-red-hat-rhel/)

    ## Fedora 23/22/21/20/19 and CentOS/RHEL 7 ##
    /usr/lib/virtualbox/vboxdrv.sh setup

### Windows
 
* Install VirtualBox

---


Setup your [default provider](https://www.vagrantup.com/docs/providers/default.html)
--------------------------

Setting up virtualbox on your example:

    export VAGRANT_DEFAULT_PROVIDER=virtualbox

Add it to your ~/.bashrc file if you want it permanent

Use it
-----

Follow up same steps as [Start](#Start)

---


Convert boxes between providers
===============================

References: 

https://github.com/sciurus/vagrant-mutate 
http://www.lucainvernizzi.net/blog/2014/12/03/vagrant-and-libvirt-kvm-qemu-setting-up-boxes-the-easy-way/

Convert to libvirt
------------------

## Dependencies 

### Fedora 23 

    sudo dnf install qemu-img libvirt-devel ruby-devel
    gem install ruby-libvirt
    
## Install 

    vagrant plugin install vagrant-mutate
    
Usage
-----

Follow up usage page: https://github.com/sciurus/vagrant-mutate#usage



    



    
