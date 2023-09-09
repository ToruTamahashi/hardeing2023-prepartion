# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

$update_rocky = <<SCRIPT
    yum update -y
SCRIPT

Vagrant.configure("2") do |config|
    ## root / root, vagrant/ vagrant
    config.vm.define "server1" do |server|
      server.vm.hostname = "rockyvm"
      server.vm.box = "tamahashi/rocky8-lamp"
      server.vm.box_version = "0.1.0"
      server.vm.network "private_network", ip: "172.31.103.10"
      server.ssh.insert_key = false
      # ローカルのファイルをvagrant環境と同期する
      # config.vm.synced_folder "ローカルの開発用ディレクトリパス", "vagrant上のディレクトリパス"
      # server.vm.synced_folder "./share", "/var/www/html"


      server.vm.provider "virtualbox" do |vb|
        # Hide the VirtualBox GUI when booting the machine
        # vb.gui = true
    
        # Customize the amount of memory on the VM:
        vb.memory = "2048"

        vb.customize [
          "modifyvm", :id,
          # ビデオメモリの割り当て
          "--vram", "256",
          # クリップボードやドラッグ&ドロップをWindowsと共有
          "--clipboard", "bidirectional",
          "--draganddrop", "bidirectional",
        ]
      end

      # server.vm.provision :shell, inline: $update_rocky
  
    end

    config.vm.define "server2" do |server|
      server.vm.hostname = "rockyeccube"
      server.vm.box = "tamahashi/rocky8-lamp"
      server.vm.box_version = "0.1.0"
      server.vm.network "private_network", ip: "172.31.103.11"
      config.vm.network "forwarded_port", guest: 80, host: 8888
      server.ssh.insert_key = false
      # ローカルのファイルをvagrant環境と同期する
      # config.vm.synced_folder "ローカルの開発用ディレクトリパス", "vagrant上のディレクトリパス"
      # server.vm.synced_folder "./share", "/var/www/html"


      server.vm.provider "virtualbox" do |vb|
        # Hide the VirtualBox GUI when booting the machine
        # vb.gui = true
    
        # Customize the amount of memory on the VM:
        vb.memory = "2048"

        vb.customize [
          "modifyvm", :id,
          # ビデオメモリの割り当て
          "--vram", "256",
          # クリップボードやドラッグ&ドロップをWindowsと共有
          "--clipboard", "bidirectional",
          "--draganddrop", "bidirectional",
        ]
      end

      # server.vm.provision :shell, inline: $update_rocky
  
    end

    config.vm.define "server3" do |server|
      server.vm.hostname = "rocky8"
      server.vm.box = "tamahashi/rocky8-lamp"
      server.vm.box_version = "0.1.0"
      server.vm.network "private_network", ip: "172.31.103.11"
      config.vm.network "forwarded_port", guest: 80, host: 8888
      server.ssh.insert_key = false
      # ローカルのファイルをvagrant環境と同期する
      # config.vm.synced_folder "ローカルの開発用ディレクトリパス", "vagrant上のディレクトリパス"
      # server.vm.synced_folder "./share", "/var/www/html"


      server.vm.provider "virtualbox" do |vb|
        # Hide the VirtualBox GUI when booting the machine
        # vb.gui = true
    
        # Customize the amount of memory on the VM:
        vb.memory = "2048"

        vb.customize [
          "modifyvm", :id,
          # ビデオメモリの割り当て
          "--vram", "256",
          # クリップボードやドラッグ&ドロップをWindowsと共有
          "--clipboard", "bidirectional",
          "--draganddrop", "bidirectional",
        ]
      end

      # server.vm.provision :shell, inline: $update_rocky
  
    end
end
