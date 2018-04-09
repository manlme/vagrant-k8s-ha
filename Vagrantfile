Vagrant.configure("2") do |config|
  config.vm.provider "parallels" do |prl|
  prl.memory = 3072
  end
  config.vm.define "master1" do |master1|
    master1.vm.box = "bento/centos-7.4"
    master1.vm.hostname = 'master1'
    master1.vm.network :private_network, ip:"10.37.129.9"
  end

  config.vm.define "master2" do |master2|
    master2.vm.box = "bento/centos-7.4"
    master2.vm.hostname = 'master2'
    master2.vm.network :private_network, ip:"10.37.129.7"
  end
  config.vm.define "master3" do |master3|
    master3.vm.box = "bento/centos-7.4"
    master3.vm.hostname = 'master3'
    master3.vm.network :private_network, ip:"10.37.129.8"
  end
  $script = <<-SCRIPT
  echo I am provisioning...
  setenforce 0
  swapoff  -a
  sed  -i /swap/d /etc/fstab
  cd /vagrant
  yum install -y *.rpm
  systemctl enable {docker,kubelet}
  systemctl start {docker,kubelet}
  cp 10-kubeadm.conf /etc/systemd/system/kubelet.service.d
  cp daemon.json /etc/docker
  cp k8s.conf /etc/sysctl.d/k8s.conf
  sysctl --system
  systemctl daemon-reload
  systemctl restart {docker,kubelet}
  SCRIPT
  config.vm.define "node1" do |node1|
    node1.vm.box = "bento/centos-7.4"
    node1.vm.hostname = 'node1'
    node1.vm.network :private_network, ip:"10.37.129.10"
    node1.vm.provision "shell", inline: $script
  end
  config.vm.define "node2" do |node2|
    node2.vm.box = "bento/centos-7.4"
    node2.vm.hostname = 'node2'
    node2.vm.network :private_network, ip:"10.37.129.11"
    node2.vm.provision "shell", inline: $script
  end
  config.vm.define "node3" do |node3|
    node3.vm.box = "bento/centos-7.4"
    node3.vm.hostname = 'node3'
    node3.vm.network :private_network, ip:"10.37.129.12"
    node3.vm.provision "shell", inline: $script
  end
  config.vm.define "node4" do |node4|
    node4.vm.box = "bento/centos-7.4"
    node4.vm.hostname = 'node4'
    node4.vm.network :private_network, ip:"10.37.129.12"
    node4.vm.provision "shell", inline: $script
  end
end
