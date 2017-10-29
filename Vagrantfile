Vagrant.configure("2") do |config|
  instances = 4
  config.ssh.insert_key = false
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = false
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.vm.box = "centos/7"
  config.vm.provider "virtualbox" do |v|
    v.memory = 3072
    v.cpus = 2
  end
  (1..instances).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.network "private_network", ip: "192.168.50.1#{i}", :netmask => "255.255.255.0"
      node.vm.hostname = "node-#{i}.hadoop.com"
      if i == instances
        node.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "./site.yml"
          ansible.inventory_path = "./hosts"
          ansible.raw_arguments  = [
             "--connection=paramiko",
             "--private-key=~/.vagrant.d/insecure_private_key"
          ] 
        end 
      end
    end
  end
  config.vm.provision :hostmanager
end
