VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.define "master" do |master|
    master.vm.network "public_network"
    master.vm.network "private_network", ip: "192.168.2.2"
    master.vm.hostname = "master"

    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/site.yml"
      ansible.sudo = true
    end
  end

  [["192.168.2.3", "0800278E158A"]].each do |ip, mac|
    config.vm.define "slave" do |slave|
      # Use a image designed for pxe boot.
      slave.vm.box = "steigr/pxe"

      # Give the host a bogus IP, otherwise vagrant will bail out.
      # Static mac address match up with dnsmasq dhcp config
      # The auto_config: false tells vagrant not to change the hosts ip to the bogus one.
      slave.vm.network "private_network", :adapter=>1, ip: "192.168.2.254", :mac => mac , auto_config: false

      # We dont need no stinking synced folder.
      config.vm.synced_folder '.', '/vagrant', disabled: true

      # Use the ip we gets assigned from dhcp when 'vagrant ssh'
      slave.ssh.host = ip
      slave.ssh.username = 'core'


      slave.vm.provider "virtualbox" do |vb, override|
        vb.gui = true
        # Chipset needs to be piix3, otherwise the machine wont boot properly.
        vb.customize ["modifyvm", :id, "--chipset", "piix3"]
      end
    end
  end
end
