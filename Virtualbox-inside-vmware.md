Notes from: http://stackoverflow.com/questions/17175696/running-vagrant-inside-vmware-vm 

You must add: 

    vhv.enable = "TRUE" 

To you .vmx config file of vmware. 

The easiest way is: 

* Got to your vmware Configuration
* Got to Datastore and browse it to the VM folder. 
* Download the .vmx file (backup it also)
* Replace the .vmx file with upload. 