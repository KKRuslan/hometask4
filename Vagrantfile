Vagrant.configure("2") do |config|
  config.vm.define "adminruslan" do |adminruslan|
    adminruslan.vm.hostname = "adminruslan"
    adminruslan.vm.box = "ubuntu/focal64"
    adminruslan.vm.network "private_network", ip: "192.168.33.10"
    adminruslan.vm.network "forwarded_port", guest: 80, host: 8888


    adminruslan.vm.provider "virtualbox" do |vb|
      vb.name = "adminruslan"
      vb.gui = false
      vb.memory = "1024"
    end

    adminruslan.vm.provision "shell", run: "always",  inline: <<-SHELL
        echo "Hello from the Ubuntu VM"
        sudo useradd -m -p '$6$ruslan$SkpBJ//kWp1XN2Jh7yyknHxHdkk.RijEWUtdmerSv4tWwTZmDITK7ES16qovy3.hPEdbBSvDWedOWvMcsCI5U/' adminuser
        sudo usermod -a -G admin adminuser
        sudo useradd -m poweruser
        sudo passwd -d poweruser
        echo 'poweruser ALL=(ALL) NOPASSWD: /usr/sbin/iptables' | sudo EDITOR='tee -a' visudo
        sudo usermod -a -G adminuser poweruser
        sudo ln -s /etc/mtab /home/poweruser/mylink
    SHELL
  end
  
end