
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 80, host: 8888
   config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     vb.gui = false
  
     # Customize the amount of memory on the VM:
     vb.memory = "2048"
   end

   config.vm.provision "shell", inline: <<-SHELL
   yum install -y epel-release
   yum install -y nginx
   
   rm -fr /usr/share/nginx/html/*
   cp -rav /vagrant/www-content/* /usr/share/nginx/html
 
   setenforce 0
   sed -ie 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config
   cat /etc/selinux/config
   systemctl start nginx
   systemctl enable nginx
   SHELL
end