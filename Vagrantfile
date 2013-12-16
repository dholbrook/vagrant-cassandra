# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
INSTANCES = 3

BOX = "opscode_ubuntu_1204_chef"
BOX_URL = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-12.04_chef-provisionerless.box"

CHEF_VERSION = "11.8.2"

MEMORY = 512

DOMAIN = "test.io"
SUBNET = "192.168.200"

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
            'listen_address' => n['addr'],
            'rpc_address' => n['addr'],
            'vnodes' => VNODES        
          }  
        }        
      end
    end
  end
end
