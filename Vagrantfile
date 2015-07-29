Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "10.12.14.16"
  config.vm.network :"forwarded_port", guest:5000, host:5000
  config.vm.provider "virtualbox" do |v|
    v.name = "devstack-test-vm"
    v.customize ["modifyvm", :id, "--memory", "2048"]
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "75"]
  end
  config.vm.provision "file", source: "./local.conf", destination: "local.conf"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "dgstack.yml"
    ansible.raw_arguments = ['-T 30', '-e pipelining=True']
  end
end
