Start
===== 

https://www.vagrantup.com/docs/getting-started/ 

Download a vagrant box 
----------------------

It will be used later for your systems, I see it like a template for new vms. 

    vagrant box add centos/7

You can check for more on [vagrant hashicorp catalog](https://atlas.hashicorp.com/boxes/search)

Setup your [default provider](https://www.vagrantup.com/docs/providers/default.html)
--------------------------

Setting up virtualbox on your example:

    export VAGRANT_DEFAULT_PROVIDER=virtualbox

Add it to your ~/.bashrc file if you want it permanent


Create a new folder to start a vm
---------------------------------

    mkdir mynewsystem1 # Create a folder to start
    cd mynewsystem1 

Now initialize as [vagrant project](https://www.vagrantup.com/docs/getting-started/project_setup.html)
----------------------------------

    vagrant init

Edit the Vagrantfile and put the name of the box you are going to use like: 

    config.vm.box = "centos/7"

Start your vm
-------------
 
    vagrant up

Now access it: 

    vagrant ssh

For More setting follow up: 

https://www.vagrantup.com/docs/vagrantfile/

    



    