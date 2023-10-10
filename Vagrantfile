# -*- mode: ruby -*-
# vi: set ft=ruby :

VIRTUAL_HOST_PRIVATE_IP_ADDRESS = "192.168.58.88"
CPU_CORES_COUNT = "2"
MEMORY_COUNT = "2048"

# create machines config
Vagrant.configure(2) do |config|
    config.vm.box = "bento/centos-8"
    config.vm.provider "virtualbox" do |v|
    config.vm.synced_folder ".", "/mnt", type: "virtualbox"
        # for connect with SSH on both machines with no password
        id_rsa_pub = File.read("#{Dir.home}/.ssh/id_rsa.pub")
        config.vm.provision "copy ssh public key", type: "shell",
        inline: "echo \"#{id_rsa_pub}\" >> /home/vagrant/.ssh/authorized_keys"
    end

  # master node config
    config.vm.define 'centos' do |centos|
        centos.vm.network :private_network, 
        ip: VIRTUAL_HOST_PRIVATE_IP_ADDRESS
        centos.vm.hostname = "centos-8"
        centos.vm.provision "shell",
        privileged: true, path: "setup.sh"
#        args: [MASTER_NODES, WORKER_NODES]
        centos.vm.provider "virtualbox" do |v|
            v.name = "centos-8"
            v.memory = MEMORY_COUNT
            v.cpus = CPU_CORES_COUNT
        end
    end

end
