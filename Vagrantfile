Vagrant.configure("2") do |config|
  servers=[
      {
        :hostname => "master",
        :box => "ubuntu/focal64",
        :ip => "192.168.56.100",
        :ssh_port => '2201'
      },
      {
        :hostname => "web01",
        :box => "ubuntu/focal64",
        :ip => "192.168.56.101",
        :ssh_port => '2202'
      },
      {
        :hostname => "web02",
        :box => "ubuntu/focal64",
        :ip => "192.168.56.102",
        :ssh_port => '2203'
      },
      {
        :hostname => "web03",
        :box => "ubuntu/focal64",
        :ip => "192.168.56.103",
        :ssh_port => '2204'
      },
      {
        :hostname => "db",
        :box => "ubuntu/focal64",
        :ip => "192.168.56.104",
        :ssh_port => '2205'
      },
      {
        :hostname => "LoadBalancer",
        :box => "ubuntu/focal64",
        :ip => "192.168.56.105",
        :ssh_port => '2206'
      }
    ]

  servers.each do |machine|
      config.vm.define machine[:hostname] do |node|
          node.vm.box = machine[:box]
          node.vm.hostname = machine[:hostname]
          node.vm.network :private_network, ip: machine[:ip]
          node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
          node.vm.provider :virtualbox do |vb|
              vb.customize ["modifyvm", :id, "--memory", 512]
              vb.customize ["modifyvm", :id, "--cpus", 1]
          end
      end
  end
end