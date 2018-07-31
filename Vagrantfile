VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "node_server" do |devenv|

    # Enable X forwarding for Selenium tests
    config.ssh.forward_x11 = true
    config.ssh.forward_agent = true

    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
      v.gui = false
    end

    devenv.vm.box = "node_server"

    devenv.ssh.username = "vagrant"
    devenv.ssh.password = "vagrant"
    devenv.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
    devenv.vm.network "private_network", ip: "192.168.222.9"

    devenv.vm.provision "ansible" do |ansible|
      ansible.playbook = "./ansible/site.yml"
      ansible.inventory_path = "ansible/hosts"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant'
      }
    end

  end

end
