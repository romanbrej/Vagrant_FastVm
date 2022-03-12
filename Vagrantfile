VAGRANT_EXPERIMENTAL="disks"

Vagrant.configure("2") do |config|
    # v2 configs...
    servers = [

        {
            :hostname => "Server1",
            :box => "ubuntu/xenial64",
            :ip => "172.17.1.50",
            :port => "2220"
        },
        
        {
            :hostname => "Server2",
            :box => "ubuntu/xenial64",
            :ip => "172.17.1.51",
            :port => "2221"
        },

        {
            :hostname => "Server3",
            :box => "ubuntu/xenial64",
            :ip => "172.17.1.52",
            :port => "2222"
        }


    ]

    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip]
            node.vm.network "forwarded_port", guest: 22, host: machine[:port], id: "ssh"
            node.vm.disk :disk, size: "20GB", primary: true
            node.vm.provision "file", source: "~/Desktop/DevOps/DevOps_Training/Linux/Webserver", destination: "$HOME"

        
            node.vm.provider "virtualbox" do |v|
                v.linked_clone = true
                v.memory = 1024
                v.cpus = 2
            end
            
            node.vm.provision "ansible" do |ansible|
                ansible.verbose = "v"
                ansible.playbook = "web_playbook.yaml"
            end
            
            
        end
  
    end
end