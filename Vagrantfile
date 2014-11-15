VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.define "master" do |vm|
    vm.vm.network "public_network"
    vm.vm.network "private_network", ip: "192.168.2.1"
    vm.vm.hostname = "master"
  end
end
