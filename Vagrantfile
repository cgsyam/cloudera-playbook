Vagrant.configure("2") do |config|
  instances = 3
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = false
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.vm.box = "centos/7"
  (1..instances).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.network "private_network", ip: "192.168.50.1#{i}", :netmask => "255.255.255.0"
      node.vm.hostname = "node-#{i}.hadoop.com"
    end
  end
  config.vm.provision :hostmanager
end

