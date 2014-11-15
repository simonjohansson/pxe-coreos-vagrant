VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.define "master" do |master|
    master.vm.network "public_network"
    master.vm.network "private_network", ip: "192.168.2.1"
    master.vm.hostname = "master"

    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/site.yml"
      ansible.sudo = true
    end
  end
end
