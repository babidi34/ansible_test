Vagrant.configure(2) do |config|

    etcHosts = ""
    ssh_config = "sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config"
    debian = "packer/packer_virtualbox-iso_virtualbox.box"
    debian11 = "debian/bullseye64"
    centos = "centos/7"
    alma8 = "almalinux/8"
    slackware = "Slackware-14.2"
  
      # set servers list and their parameters
    NODES = [
        { :hostname => "serveur-debian11", :ip => "192.168.56.60", :cpus => 1, :mem => 1024, :os => debian11, :size_disk => "60GB" },
        { :hostname => "serveur-alma8", :ip => "192.168.56.61", :cpus => 1, :mem => 1024, :os => alma8, :size_disk => "25GB" },
        { :hostname => "serveur-centos7", :ip => "192.168.56.62", :cpus => 1, :mem => 1024, :os => centos, :size_disk => "25GB" },
      ]
      
      # define /etc/hosts for all servers
    NODES.each do |node|
      etcHosts += "echo '" + node[:ip] + "   " + node[:hostname] + "' >> /etc/hosts" + "\n"
      
    end #end NODES
    
      # run installation
    NODES.each do |node|
      config.vm.define node[:hostname] do |cfg|
        cfg.vm.box = node[:os]
        cfg.vm.hostname = node[:hostname]
        cfg.vm.network "private_network", ip: node[:ip]
        cfg.disksize.size = node[:size_disk]
        cfg.vbguest.auto_update = true
        cfg.vm.provider "virtualbox" do |v|
          v.customize [ "modifyvm", :id, "--cpus", node[:cpus] ]
          v.customize [ "modifyvm", :id, "--memory", node[:mem] ]
          v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
          v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
          v.customize ["modifyvm", :id, "--name", node[:hostname] ]
        end #end provider
        
          #for all
        cfg.vm.provision "file", source: "docker_key.pub", destination: "/home/vagrant/.ssh/docker_key.pub"
        cfg.vm.provision "shell", inline: <<-SHELL
          mkdir -p /home/vagrant/.ssh
          cat /home/vagrant/.ssh/docker_key.pub >> /home/vagrant/.ssh/authorized_keys
          chown -R vagrant:vagrant /home/vagrant/.ssh
          chmod 600 /home/vagrant/.ssh/authorized_keys
        SHELL
        cfg.vm.provision :shell, :inline => etcHosts
      end # end config
    end # end nodes
  end