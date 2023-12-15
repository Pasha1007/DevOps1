Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.define "centos7" do |box|
  box.vm.box = "centos/7"
  box.vm.box_version = "2004.01"
  box.vbguest.installer_options = { allow_kernel_upgrade: true }
  end
  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.ssh.insert_key = false
  config.vm.synced_folder "web", "/usr/share/nginx/index.html", type: "rsync", mount_options: ["-o", "uid=nginx", "-o", "gid=nginx", "--chmod=ug=rwX,o=rX"]
  config.vm.provision "shell", inline: <<-SHELL
    yum install -y epel-release
    yum install -y nginx
    setenforce 0
    sed -ie 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config
    systemctl enable nginx
    systemctl start nginx
    systemctl restart nginx

  SHELL

end