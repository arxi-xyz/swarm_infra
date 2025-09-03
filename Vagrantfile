require 'yaml'

VAGRANT_DIR = File.dirname(__FILE__)
CONFIG = YAML.load_file(File.join(VAGRANT_DIR, "config", "vagrant.yml"))


Vagrant.configure("2") do |config|
  CONFIG["vms"].each do |name, settings|
    config.vm.define name do |vm|
      vm.vm.box = "debian/bookworm64"
      vm.vm.hostname = name
      vm.vm.network "private_network", ip: settings["ip"]

      vm.vm.provider "virtualbox" do |vb|
        vb.cpus = settings["cpus"]
        vb.memory = settings["memory"]
      end
    end
  end

  config.ssh.insert_key = false
  config.ssh.private_key_path = [
    "~/.vagrant.d/insecure_private_key",
    "~/.ssh/id_rsa"
  ]
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = File.join(VAGRANT_DIR,"ansible", "playbooks", "vagrant_initial_setup.yml")
    ansible.vault_password_file = File.join(VAGRANT_DIR,"ansible", "vault", "vault_pass.txt")
    ansible.groups = {
      "all_vms" => ["minikube-vm"]
    }
  end
  
end