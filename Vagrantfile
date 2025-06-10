Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-24.04"

  config.vm.define "dns-node" do |dns|
    dns.vm.hostname = "dns-node"
    dns.vm.network "private_network", ip: "192.168.56.20"
    dns.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end
    dns.vm.provision "ansible" do |ansible|
      ansible.playbook = "dns-playbook.yml"
      ansible.extra_vars = { ansible_python_interpreter: "/usr/bin/python3" }
    end
  end

  config.vm.define "k3s-master" do |k3s|
    k3s.vm.hostname = "k3s-master"
    k3s.vm.network "private_network", ip: "192.168.56.10"
    k3s.vm.provider "virtualbox" do |vb|
      vb.memory = 8192
      vb.cpus = 4
    end
    k3s.vm.provision "ansible" do |ansible|
      ansible.playbook = "k3s-playbook.yml"
      ansible.extra_vars = {
        ansible_python_interpreter: "/usr/bin/python3",
        user_home: "/home/vagrant"
      }
    end
  end
end
