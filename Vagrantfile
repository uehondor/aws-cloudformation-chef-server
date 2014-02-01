# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu-quantal64"
    config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/quantal/20140129/quantal-server-cloudimg-amd64-vagrant-disk1.box"

    config.vm.network :private_network, ip: "192.168.33.10"
    config.ssh.forward_agent = true

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1024", '--cpus', '2']
    end

    config.berkshelf.enabled = true

    config.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "chef/cookbooks"

        chef.add_recipe "chef-server::default"

        chef.json = {
            "chef-server" => {
                :api_fqdn => "192.168.33.10",
                :configuration => {
                    :version => :latest,
                    :chef_server_webui => {
                        :enable => true
                    }
                }
            }
        }
    end

    config.vm.provision "shell", path: "chef/copy_keys.sh"
end
