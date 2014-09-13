# Vagrant Cassandra

This is a sample project to show how to get a simple Cassandra cluster up and running with Vagrant.  It is not secure or production ready.

## Acknowledgement

I borrowed ideas from an earlier project on github [vagrant-cassandra](https://github.com/calebgroom/vagrant-cassandra).  The Vagrant code style was highly influenced by [mcollective-vagrant](https://github.com/ripienaar/mcollective-vagrant).

## Prerequisites

* [Virtualbox](https://www.virtualbox.org/)
* [Vagrant](http://www.vagrantup.com/)
* [librarian-chef](https://github.com/applicationsonline/librarian-chef)
* [vagrant-omnibus](https://github.com/schisamo/vagrant-omnibus)

## Usage

The first time you use this you need to installed the required chef recipes with `librarian-chef`.

    $librarian-chef install
    Installing apt (2.3.0)
    Installing ark (0.4.0)
    Installing aws (1.0.0)
    Installing chef_handler (1.1.4)
    Installing firewall (0.11.2)
    Installing windows (1.11.0)
    Installing java (1.16.4)
    Installing ufw (0.7.0)
    Installing yum (3.0.0)
    Installing cassandra (2.0.0)
    
After that you should be able to interact with the Cassandra nodes.
 
	vagrant@node2:~$ cqlsh
	Connected to Test Cluster at localhost:9160.
	[cqlsh 4.1.1 | Cassandra 2.0.9 | CQL spec 3.1.1 | Thrift protocol 19.39.0]
	Use HELP for help.
	cqlsh> 
	
	vagrant@node2:~$ nodetool status
	Datacenter: datacenter1
	=======================
	Status=Up/Down
	|/ State=Normal/Leaving/Joining/Moving
	--  Address         Load       Tokens  Owns (effective)  Host ID                               Rack
	UN  192.168.200.11  77.9 KB    256     63.9%             f54bd369-452e-4474-bae3-69b564b1c0c7  rack1
	UN  192.168.200.13  85.45 KB   256     67.8%             739ee255-0436-4c28-aae4-c8c6fc9a2c7b  rack1
	UN  192.168.200.12  60.11 KB   256     68.4%             f2561d69-2f5c-423b-8a93-16d39177ea59  rack1
    
##Changelog

**2014-09-13**

* upgrade Ubuntu from 12.04 to 14.04
* upgrade Chef to from 11.8.2 to 11.16.0
* upgrade Cassandra from 2.0.3 to 2.0.9
* upgrade java from 1.7.0\_51 to 1.7.0\_67
* increased RAM from 512 to 1024
* switch from cassandra::tarball to cassandra::datastax
* add apache2 licence
* add explicit versions to Cheffile
* add `ssl_verify_mode = :verify_peer` configuration to remove chef warning


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/dholbrook/vagrant-cassandra/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

