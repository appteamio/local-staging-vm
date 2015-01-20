# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = '2'
Vagrant.require_version '>= 1.5.0'
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = 'stag-vm'
  config.omnibus.chef_version = 'latest'
  config.vm.box = 'ubuntu/trusty64'
  config.vm.network :private_network, type: 'dhcp'
    config.vm.network "private_network", ip: "192.168.50.38"
  config.vm.synced_folder "./data", "/data"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = [:host, "cookbooks"]
    chef.provisioning_path = "/vagrant-chef"
    chef.json = {
       app: "feather",
       group: "vagrant",
       user: {
                  name: "vagrant",
                  email: "jalil@appteam.io" 
                },
       git:{
                  name: "appteamio",
                  email: "jalil@appteam.io" 
                  },
       db: {
              root_password: "iwantobelive",
            }
    }
    chef.run_list = [
      'recipe[crockpot::default]',
      'recipe[crockpot::nodejs]',
      'recipe[crockpot::rbenv]',
      'recipe[crockpot::mysql]',
      'recipe[crockpot::php]',
      'recipe[crockpot::nginx]',
      'recipe[crockpot::gitconf]',
      'recipe[crockpot::app]'

    ]
  end
end