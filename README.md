# Vagrant Docker provisioner

Demo Vagrant with Docker provisioner.

Requirements
------------

* Vagrant
* VirtualBox

Run the application
-------------------

Up and running:

	vagrant up

If plugin vagrant-proxyconf is installed, reload to configure the proxy for Docker:

	vagrant provision

Go to http://127.0.0.1:4567/.

Configure your corporate proxy
------------------------------

Install [Proxy Configuration Plugin](http://tmatilai.github.io/vagrant-proxyconf/) for Vagrant:

	vagrant plugin install vagrant-proxyconf

Create a Vagrantfile in your home folder:

	$HOME/.vagrant.d/Vagrantfile

With:

	Vagrant.configure("2") do |config|
		if Vagrant.has_plugin?("vagrant-proxyconf")
			config.proxy.http     = "http://proxy.example.com:8080/"
			config.proxy.https    = "http://proxy.example.com:8080/"
			config.proxy.no_proxy = "localhost,127.0.0.1"
		end
	end

Add environment variables:

	export http_proxy=http://proxy.example.com:8080/
	export https_proxy=http://proxy.example.com:8080/
