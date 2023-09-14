Vagrant.configure("2") do |config|
    config.vm.define "server1" do |server|
      server.vm.hostname = "rockypress"
      server.vm.box = "tamahashi/rocky8-wordpress"
      server.vm.box_version = "0.2.1"
      server.vm.network "private_network", ip: "172.31.103.10"
      server.vm.network "forwarded_port", guest: 80, host: 8888, id: "http"
      server.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"
      server.ssh.insert_key = false

      # HostOSとGuestOSのファイル同期
      # config.vm.synced_folder "ローカルの開発用ディレクトリパス", "vagrant上のディレクトリパス"
      # server.vm.synced_folder "./share", "/var/www/html"

      server.vm.provider "virtualbox" do |vb|
        # GUIがあるサーバーのときはtrue
        # vb.gui = true
    
        # メモリサイズ割り当て
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
    end

    config.vm.define "server2" do |server|
      server.vm.hostname = "rockycube"
      server.vm.box = "tamahashi/rocky8-eccube"
      server.vm.box_version = "0.2.0"
      server.vm.network "private_network", ip: "172.31.103.11"
      server.vm.network "forwarded_port", guest: 80, host: 8889, id: "http"
      server.vm.network "forwarded_port", guest: 22, host: 2223, id: "ssh"
      server.ssh.insert_key = false


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
    end
end
