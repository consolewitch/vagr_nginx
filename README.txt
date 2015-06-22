This will guide you through using Ansible and Vagrant to automate the
creation of an NginX web server. Configuration options will allow you 
to specify a git repository that will automatically be pulled down and
placed in the webroot of your server as well as the port at which you
want to serve your site. Please note that the playbook is kept in a 
separate repository from the vagrantfile in case the former needs to
be used without the latter. Consequently you will need to pull down both
repositories.

Quick Start:
============
    # git clone https://github.com/logicalmethods/vagr_nginx.git
    # git clone https://github.com/logicalmethods/ans_nginx.git
    # ln -s ../ans_nginx/ vagr_nginx/ans_nginx
    # cd vagr_nginx;vagrant up


Requirements:
=============

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


Warnings:
=========

1) This playbook will disable the IPTables firewall on the target host.
2) Running this playbook will temporairly stop your NginX server.
3) Other NginX sites running on this server will be disabled. (see notes)


Set Up:
=======
note: These instructions have been tested on Linux and OS X, Windows
mileage may vary.

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

	gitRepo: https://github.com/puppetlabs/exercise-webpage #Git repo containing html to serve.
    	portNumber: 8000 	#Port upon which to serve the repo.


Starting the box:
=================
	From inside the vagr_nginx directory type the following command:
	# vagrant up

	as the script completes it will give you the address where you can
	access the new web server.


Refreshing the box:
===================
	If you want to update the HTML from git, you need to ask vagrant
	to re-run the ansible playbook. use this command from inside the
	vagr_nginx directory:
	# vagrant provision


Notes:
======
	If you run this script against a server that is already serving
	nginx files, it will disable all your other sites in favor of its
	own. If this happens accidentally it is easy to fix, simply 
	create symbolic links from /etc/nginx/conf.available/site.conf to
	/etc/nginx/conf.d

	This playbook is designed for Centos 6.x. Centos 7 introduced
	systemd and some other technologies that may not be compatible.
	It will not run on Ubuntu and has not been tested on any other
	Linux distribution.

-=-
2015/06/16
alex@speaks.io
    


