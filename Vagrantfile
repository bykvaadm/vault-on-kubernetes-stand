Vagrant.configure("2") do |config|
  config.vm.base_mac = nil
  config.vm.synced_folder ".", "/vagrant", disabled: false

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
    vb.linked_clone = true
  end

  config.vm.define "master" do |n|
    n.vm.box = "ubuntu/xenial64"
    n.vm.hostname = "master"
    n.vm.network "private_network", ip: "192.168.77.10"
  end

  N = 3
  (1..N).each do |machine_id|
    config.vm.define "node-#{machine_id}" do |n|
      n.vm.hostname = "node-#{machine_id}"
      n.vm.network "private_network", ip: "192.168.77.#{20+machine_id}"
      n.vm.box = "ubuntu/xenial64"

      if machine_id == N
        n.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "site.yaml"
          ansible.groups = {
            "kubernetes" => [ "master", "node-[1:#{N}]" ],
            "kubernetes-master" => [ "master" ],
            "kubernetes-node" => [ "node-[1:#{N}]" ]
          }
          ansible.raw_arguments = [ "-D" ]
        end
      end
    end
  end
end
