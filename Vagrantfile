VAGRANTFILE_API_VERSION = "2"

cluster = {
  "mesos-master-1" => { :ip => "192.168.1.10", :cpus => 1, :mem => 1024 },
  "mesos-master-2" => { :ip => "192.168.1.11", :cpus => 1, :mem => 1024 },
  "mesos-slave-1" => { :ip => "192.168.1.20", :cpus => 1, :mem => 1024 },
  "mesos-slave-2" => { :ip => "192.168.1.21", :cpus => 1, :mem => 1024 },
  "zookeeper" => { :ip => "192.168.1.30", :cpus => 1, :mem => 1024 },
  "aurora" => { :ip => "192.168.1.40", :cpus => 1, :mem => 1024 }
}
 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  cluster.each_with_index do |(hostname, info), index|

    config.vm.define hostname do |cfg|
      cfg.vm.provider :virtualbox do |vb, override|
        config.vm.box = "debian/jessie64"
        override.vm.network :private_network, ip: "#{info[:ip]}"
        override.vm.hostname = hostname
        vb.name = hostname
        vb.customize ["modifyvm", :id, "--memory", info[:mem], "--cpus", info[:cpus], "--hwvirtex", "on"]
      end # end provider
    end # end config

  end # end cluster
end
