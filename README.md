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
	Installing chef_handler (1.1.6)
	Installing windows (1.34.2)
	Installing 7-zip (1.0.2)
	Installing apt (2.6.0)
	Installing ark (0.9.0)
	Installing java (1.28.0)
	Installing ulimit (0.3.2)
	Installing yum (3.3.2)
	Installing cassandra (2.8.0)
	Installing firewall (0.11.8)
	Installing ufw (0.7.4)
    
After that you should be able to interact with the Cassandra nodes.
 
    vagrant@node2:~$ cqlsh
    Connected to Test Cluster at 127.0.0.1:9042.
    [cqlsh 5.0.1 | Cassandra 2.1.0 | CQL spec 3.2.0 | Native protocol v3]
    Use HELP for help.
    cqlsh>
	
    vagrant@node2:~$ /usr/local/cassandra/bin/nodetool status
    Datacenter: datacenter1
    =======================
    Status=Up/Down
    |/ State=Normal/Leaving/Joining/Moving
    --  Address         Load       Tokens  Owns (effective)  Host ID                               Rack
    UN  192.168.200.11  54.88 KB   256     65.6%             9d3e59d5-27b8-4d45-9ac1-1e1b3a9c6df1  rack1
    UN  192.168.200.13  111.8 KB   256     66.9%             c8e91f28-42d2-452e-8b27-311e70b34987  rack1
    UN  192.168.200.12  122.65 KB  256     67.4%             f5ceccc8-3e40-406b-9a7c-92c1b6cb4bb5  rack1
    
##Changelog

**2014-10-11**

* upgrade cassandra-chef-cookbook to 2.8.0
* set cassandra version to 2.1.0
* switch back to cassandra::tarball
* remove cassandra restart post provisioner

**2014-09-13**

* upgrade Ubuntu from 12.04 to 14.04
* upgrade Chef to from 11.8.2 to 11.16.0
* upgrade Cassandra from 2.0.3 to 2.0.9
* upgrade java from 1.7.0\_51 to 1.7.0\_67
* increased RAM from 512 to 1024
* switch from cassandra::tarball to cassandra::datastax
* add apache2 license
* add explicit versions to Cheffile
* add `ssl_verify_mode = :verify_peer` configuration to remove chef warning


