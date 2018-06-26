VAGRANTFILE_API_VERSION = "2"

required_plugins = %w( vagrant-hostmanager vagrant-docker-compose )
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

Vagrant.configure(2) do |config|

  config.vm.box = "bento/ubuntu-16.04"
  config.vm.network "private_network", ip: "192.168.50.100"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.vm.hostname = "livecode.local"

  # VirtualBox specific configuration
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: "/vagrant/docker-compose-vagrant.yml", rebuild: true, run: "always"

end
