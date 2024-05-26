machines = {
    "master" => {"memory" => "1024", "cpu" => "1", "ip" => "100", "image" => "ubuntu"}
    "node1" => {"memory" => "1024", "cpu" => "2", "ip" => "101", "image" => "ubuntu"}
    "node2" => {"memory" => "1024", "cpu" => "2", "ip" => "102", "image" => "ubuntu"}
    "node3" => {"memory" => "1024", "cpu" => "2", "ip" => "103", "image" => "ubuntu"}
}

Vagrant.configure("2") do |config|

    machines.each do |name, conf|
        config.vm.define "#{name}" do |machine|

            machine.vm.box = "#{conf["image"]}"
            machine.vm.network "private_network", ip: "192.168.10.#{conf["ip"]}"
            machine.vm.hostname = "#{name}"

            machine.vm.provider "virtualbox" do |v|
                v.name = "#{name}"
                v.cpus = conf["cpu"]
                v.memory = conf["memory"]
            end

            machine.vm.provision "shell", path: "docker.sh"

            if "#{name}" == "master"
                machine.vm.provision "shell", path: "master.sh"
            else
                machine.vm.provision "shell", path: "worker.sh"
            end
            
        end
    end
end