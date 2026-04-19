Vagrant.configure("2") do |config|

  config.vm.define "kali" do |kali|
    kali.vm.box = "kalilinux/rolling"
    kali.vm.hostname = "kali"
    kali.vm.network "private_network", ip: "192.168.56.10"
    kali.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
      vb.name = "kali-attacker"
    end
  end

  config.vm.define "target" do |target|
    target.vm.box = "ubuntu/jammy64"
    target.vm.hostname = "target"
    target.vm.network "private_network", ip: "192.168.56.20"
    target.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
      vb.name = "ubuntu-target"
    end
  end

end