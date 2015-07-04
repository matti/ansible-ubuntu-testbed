Vagrant.configure(2) do |config|
  config.vm.define "proxy" do |proxy|
    proxy.vm.box = "ubuntu/trusty64"

    proxy.ssh.port = "2200"
    config.vm.network :forwarded_port, guest: 22, host: 2200, id: 'ssh'

    config.vm.provider "virtualbox" do |vbox|
      vbox.memory = 512
      vbox.cpus = 2
    end
  end

  config.vm.define "app" do |web|
    web.vm.box = "ubuntu/trusty64"

    web.ssh.port = "2210"
    config.vm.network :forwarded_port, guest: 22, host: 2210, id: 'ssh'

    config.vm.provider "virtualbox" do |vbox|
      vbox.memory = 1024
      vbox.cpus = 2
    end
  end

  # for all machines
  config.vm.provision :shell, path: "bootstrap.sh"
end
