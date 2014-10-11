# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
CASSANDRA_VERSION = "2.1.0"
CHEF_VERSION = "11.16.0"

BOX = "opscode_ubuntu-14.04_chef-provisionerless"
BOX_URL = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"

INSTANCES = 3
MEMORY = 1024
DOMAIN = "example.org"
SUBNET = "192.168.200"
CLUSTER_NAME = "Test Cluster"

SEEDS = []
NODES = []
VNODES = 256

INSTANCES.times do |i|
  name = "node%d" % (i + 1)
  hostname = "#{name}.#{DOMAIN}"
  addr = "#{SUBNET}.%d" % (10 + i + 1)
  NODES << {
    'name' => name,
    'hostname' => hostname,
    'addr' => addr,
    'token' => 256
  }
  SEEDS << addr
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|  
  NODES.each do |n|
    config.vm.define n['name'] do |node|
      node.vm.box = BOX
      node.vm.box_url = BOX_URL      
      node.omnibus.chef_version = CHEF_VERSION
      node.vm.network :private_network, ip: n['addr']
      node.vm.hostname = n['hostname']
      node.vm.provider :virtualbox do |vb|
        vb.name = "vagrant_cassandra_#{n['name']}"
        vb.customize ["modifyvm", :id, "--memory", MEMORY]
      end
      node.vm.provision :chef_solo do |chef|
        chef.custom_config_path = "Vagrantfile.chef"
        chef.cookbooks_path = ["chef/cookbooks", "chef/site-cookbooks"]
        chef.roles_path = "chef/roles"
        chef.data_bags_path = "chef/data_bags"
        chef.add_recipe "apt"  
        chef.add_recipe "java"
        chef.add_recipe "ufw::disable"
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
            'version' => CASSANDRA_VERSION,
            'seeds' => SEEDS,
            'listen_address' => n['addr'],
            'broadcast_address' => n['addr'],
            'rpc_address' => '0.0.0.0',
            'vnodes' => VNODES,
            'cluster_name' => CLUSTER_NAME  
          }  
        }        
      end
      # Bind port configuration not detected until restart for unknown reasons
      # use shell provisioner as workaround
      # node.vm.provision :shell, :inline => "sudo service cassandra restart"
    end
  end
end
