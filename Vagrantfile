INSTANCES=3

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.ssh.insert_key = false
  (1..INSTANCES).each do |i|
    config.vm.define "centos#{i}" do |node|

      node.vm.network "private_network", ip: "192.168.56.#{i+10}"
      node.vm.hostname = "centos#{i}.mito.local"
      node.vm.synced_folder "./provision/", "/provision/", create: true

      node.vm.provision "ansible_local" do |ansible|
          ansible.provisioning_path = "/provision/"
          ansible.become = true
          ansible.playbook = "init.yml"
      end
    end 
  end
end