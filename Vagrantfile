Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "4098"
    vb.cpus = 4
  end

  config.vm.define "jenkins-vm" do |jenkins|
    jenkins.vm.network :private_network, ip: "192.168.1.12"
  end
end
