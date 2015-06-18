This will guide you through using Ansible and Vagrant to automate the
creation of an NginX web server. Configuration options will allow you 
to specify a git repository that will automatically be pulled down and
placed in the webroot of your server. Please note that I prefer to
develop my playbooks seperately from my vagrantfiles in case the 
former needs to be used without the latter. Consequently you will need 
to pull down two code repositories. The instructions below will guide you.


Before you even start:
======================

Before you can use this ansible provisioned vagrant box, make sure
you have the following software packages installed and configured on 
your workstation. There is a lot of help available on the internet
if you're not sure how to do this:

    Virtualbox  http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html
    Git         http://git-scm.com/downloads
    Vagrant     https://www.vagrantup.com/downloads.html
    Ansible     http://docs.ansible.com/intro_installation.html

You will also need an internet connection that is accessible from your
virtual machines and does not block web traffic.


Setting up the box:
===================

1) Clone and link the necessary repositories:
    Clone the vagr_nginx repo from Github:
    # git clone https://github.com/logicalmethods/vagr_nginx.git
    Clone the ans_nginx repo from Github:
    # git clone https://github.com/logicalmethods/ans_nginx.git
    Create a symbolic link between the universal vagrant box
    # ln -s ../ans_nginx/ vagr_nginx/ans_nginx

2) Configure the box to fit your needs:
    Edit the vars.yml file inside of the vagr_nginx folder to
    choose your desired configuration. Here is a sample vars.yml.

		gitRepo: https://github.com/puppetlabs/exercise-webpage #A git repo containing html you want to serve.
    	portNumber: 8000 	#The port upon which you want to serve your repo.


Starting the box:
=================
	From inside the vagr_nginx direcotry type the following command:
	# vagrant up

	as the script completes it will give you the address where you can
	access the new web server.


Refreshing the box:
===================
	If you want to update the server all you need to do is ask vagrant
	to re-run the ansible playbook. use this command from inside the
	ans_nginx directory:
	# vagrant provision


Notes:
======
	The ans_nginx playbook disables the iptables firewall on a linux
	server. This can be a security problem. If you're planning to run
	this box in production please take additional precautions to
	secure your system.


-=-
2015/06/16
alex@speaks.io
    


