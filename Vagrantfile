Vagrant.configure(2) do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.network :forwarded_port, guest: 8080, host: 4567
  
  # Fix unattended updates locking dpkg : https://github.com/chef/bento/issues/609
  config.vm.provision "shell", inline: "rm /var/lib/apt/lists/lock"
  config.vm.provision "shell", inline: "rm /var/cache/apt/archives/lock"
  
  config.vm.provision "docker" do |d|
    # Set build-time variables
    build_image_args =  "-t helloworld"
    if ENV.has_key?('http_proxy') && ENV.has_key?('https_proxy')
      build_image_args = build_image_args + " --build-arg http_proxy=" + ENV['http_proxy']
      build_image_args = build_image_args + " --build-arg https_proxy=" + ENV['https_proxy']
    end

    # Build image and run container
    d.build_image "/vagrant/src",
      args: build_image_args
    d.run "helloworld",
      args: "-p 8080:8080"
  end
end