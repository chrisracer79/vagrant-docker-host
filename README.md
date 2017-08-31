This project uses Vagrant to set up a Centos7 virtualbox machine with Docker installed to be used specifically with LearnWebLogicOnline.com's series of Oracle and Docker training courses.

Requirements
1. Virtualbox 4.0 or greater installed
2. Vagrant installed
3. git installed (optional)

Steps

1. Clone this repository or copy the Vagrantfile to a directory on your computer
2. In a command or terminal window run the following command in the directory where you placed the Vagrantfile:
    > vagrant up
    
vagrant up will start downloading a CentOS 7 base box and begin configuring the VM to use docker. This will take some considerable time. 

3. You will know the VM has been created successfully when you see the docker container hello-world running. 

4. Once the vagrant up command completes, log into the VM using vagrant ssh. This VM is set up to use ssh keys for authentication.

5. This VM can now be used as your docker host for the WebLogic on Docker lab exercises.

Stopping the VM
In the Vagrantfile directory, run 'vagrant halt' to stop the VM.

Starting the VM
In the Vagrantfile directory, run 'vagrant reload' to start the VM again without rebuilding.

Destorying the VM
To destroy and delete the VM and its disk, run 'vagrant destory'. This command will completely remove the vagrant box.

Getting Files in and Out of the Virtual Machine
1. Using SCP.  You can use scp to secure copy files in and out of the virtual machine. Since ssh on the VM has been set up to use SSH keys, you have to configure your SCP client to use the ssh private key that was generated during the vagrant up. 
To find this key, run this command in the Vagrantfile directory. 

> vagrant ssh-config

Note the path of the private key.  You will use this private key in your scp client.  

For Windows I recommend using WinSCP. WinSCP will have to conver the format of the private key to a PuTTy (ppk) format. It will do this automatically for you.

For Linux and OSX, scp is already available.

