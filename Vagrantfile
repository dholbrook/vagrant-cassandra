# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

ADDRESS = "192.168.200.11"
SEEDS = []
SEEDS << ADDRESS

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.omnibus.chef_version = "11.8.2"

  config.vm.box = "opscode_ubuntu_1204_chef"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-12.04_chef-provisionerless.box"

  config.vm.network :private_network, ip: ADDRESS

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["chef/cookbooks", "chef/site-cookbooks"]
    chef.roles_path = "chef/roles"
    chef.data_bags_path = "chef/data_bags"
    chef.add_recipe "apt"  
    chef.add_recipe "java"
    chef.add_recipe "cassandra::tarball"
    chef.json = {
      :java =>  {
        'install_flavor' => 'oracle',
        'jdk_version' => '7',
        'oracle' => {
          'accept_oracle_download_terms' => true
        }
      },
      :cassandra => {
        'version' => '2.0.3',
        'seeds' => SEEDS,
        'listen_address' => ADDRESS,
        'rpc_address' => ADDRESS,        
      }  
    }
  end
  
end
