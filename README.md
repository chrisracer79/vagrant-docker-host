This project uses Vagrant to set up a Centos7 virtualbox machine with Docker installed to be used specifically with LearnWebLogicOnline.com's series of Oracle and Docker training courses.

Requirements
1. Virtualbox 4.0 or greater installed
2. Vagrant installed
3. git installed (optional)

Steps
This lab is intended to show students another way, perhaps a more efficient way, of setting up a docker host on a virtual machine using vagrant and the supplied Vagrantfile.  The Vagrantfile that accompanies this course takes care of provisioning a CentOS 7 virtual machine along with installing docker. In this lab you will download the Vagrantfile and provision a VM using this Vagrantfile. 

This VM will then become your docker host and be used through the remainder of this course. 

Ok so here we go

	1. Install Vagrant for your operating system
		a. https://www.vagrantup.com/downloads.html
		b. For this lab we're using 1.9.8
	2. Create a vagrant directory in your home directory to keep things simple. Call it vagrant-docker.
	3. Copy the Vagrantfile from the course resources or from github into vagrant-docker
	4. Open a command window and change to the vagrant-docker directory
	5. Run vagrant up to build and launch the VM.
		a. The first time vagrant up runs will take quite a while as vagrant will download a virtualbox and configure it per the instructions in the Vagrantfile.
		b. The build process installs git and docker along with any required libraries.
		c. The final output of the VM build should be output from the hello-world container. This verifies that docker has been successfully installed and ready for use. 
	6. Once the vagrant up command returns the VM is launched, be sure to log into the machine as 'vagrant' user using the vagrant ssh command.
		a. The build process configured a vagrant user along with SSH keys so you do not need to specify a password when logging in. 
	7. Run docker images to verify the hello-world image exists.

You know have a centos7 virtual machine that you can use as your docker host. 

Shutting Down and Restarting the VM
You can stop the VM by running the vagrant halt command. This will send a signal to the VM to gracefully shutdown.

To restart the VM you run 'vagrant reload' or 'vagrant up'

Connecting to the Docker Host
Download PuttY and its various utils from here

https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

We are going to need PuTTy and PuTTygen. 

In the last lab you connected to the VM using vagrant ssh which logged you into the VM as the user 'vagrant' using a generated private key. This is the account you will use for all the lab exercises. You will need to know the location of the private key in order to use PuTTy or any other client using ssh to connect to the VM.

In a command window go to the vagrant-docker diretory and run vagrant ssh-config
Note the Port number is 2222 and the location of the identity file. The identity file is the private key. You will use this path when configuring an ssh connection to the server.

Next we need to convert the private key to a format that PuTTy understands. Use PuTTygen to convert the key to a ppk format and save it anywhere you wish. 
Launch PUTTYgen 
Click Load then locate the private key you want to convert.
The key should appear in PuTTYgen. 
Click the Save private key button. Save this key with the name private_putty_key.ppk

Now launch PuTTy
On the left hand side, find the SSH category and expand it. 
Click on Auth under SSH. 
On the right hand side you will see a the parameter Private key file for authentication. Click on the Browse button and locate the ppk file you just created.
On the left side, go back to Session
Enter localhost for the hostname and 2222 for the port
Enter a nice descriptive name in the Saved Sessions field and click Save. 
Now click Open. Verify you are able to connect to the VM.

Transferring Files to and From the Docker Host
The simplest way to transfer files from the Docker host to the virtual machine is to place the files in the same directory as the Vagrantfile. When the VM is booted by vagrant, a one-time rsync is performed copying all the files from the host to virtual machine. These files will appear under /vagrant. 

In this lab you will be downloading installation packages for Oracle JRE and WebLogic. You can copy these packages to the Vagrantfile directory prior to starting your VM.  After the VM the packages will appear on the docker host. 

Another method for transferring files is to use secure copy or scp. If you are not familiar with scp, it uses ssh as the underlying protocol. For Windows environments, I recommend using the WinSCP application.
https://winscp.net/eng/download.php

While either method works, secure copy is more efficient since we do not have to restart the VM in order to perform the sync. There other methods of sharing and exporting folders through VirtualBox and NFS, but these methods are out of scope for this lab. 


	
