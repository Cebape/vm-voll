# -*- mode: ruby -*-
	# vi: set ft=ruby :
	#

	#
	# Include box configuration from YAML file boxes.yml
	#
	require 'yaml'
	settings = YAML.load_file 'vagrant.yml'

	Vagrant.configure("2") do |config|
	    #
	    # Configuração Genérica, válida para todas as vm's
	    #
	  
	    # Check vbox update
	    #
	    # see local vboxes: $ vagrant box list
	    #
	    config.vm.box_check_update = false

	    # PC-Developer Network Interface:
	    config.vm.network "public_network", ip: settings['ip_address'], bridge: settings['name_bridge']
	 
	    #
	    # define app vbox (VM-Work)
	    #
	    config.vm.define :voll do |app_config|
	      #
	      # vm-vagrant distro: Official Ubuntu 20.04 LTS
	      app_config.vm.box = settings['type_vbox']

	      # vm-vagrant vbox upadate
	      app_config.vm.box_check_update = false

	      #
	      # Sync App Folder
	      #
	      app_config.vm.synced_folder "./sync_folder_host", "/home/vagrant/sync_folder_work", create: true
	 
	      # define hostname: developer / operator / tester / release / product / ...
	      #
	      app_config.vm.hostname = settings['vm_hostname']
	      #
	      #
	      app_config.vm.provider "virtualbox" do |ap|
		#
		# define tamanho da memória RAM da VM
		#
		ap.customize ["modifyvm", :id, "--memory", "1024"]
		#
		# Projeto: nome da vm-vagrant
		#
		ap.name = settings['vm_name']
	      end
	      #
	      # Atualização & Provisionamento
	      #
	      app_config.vm.provision :shell, inline: "echo Provisionamento da vbox"
	      #
	      app_config.vm.provision "ansible" do |ansible|
	        ansible.playbook =   settings['ansible_path']  
	        ansible.verbose = "v"
	      end
	      #
	      #
	    end
	    #
	    #
	  end
       