Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.define "centos7" do |box|
  box.vm.box = "centos/7"
  box.vm.box_version = "2004.01"
  box.vbguest.installer_options = { allow_kernel_upgrade: true }
  end
  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.ssh.insert_key = false
  #config.vm.synced_folder "web", "/usr/share/nginx/html"
  config.vm.synced_folder "web", "/usr/share/nginx/html", type: "rsync", mount_options: ["-o", "uid=nginx", "-o", "gid=nginx", "--chmod=ug=rwX,o=rX"]
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum install -y epel-release
    sudo yum install -y nginx
    sudo systemctl enable nginx
    sudo systemctl start nginx
    # sudo rm -rf /usr/share/nginx/html/index.html
    # sudo chown nginx:nginx /usr/share/nginx/html/index.html
    # sudo chmod -R 755 /usr/share/nginx/html
    sudo systemctl restart nginx
  SHELL

end