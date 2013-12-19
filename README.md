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
    
 After that you should be able to bring up the VMs with vagrant.
 
    $vagrant up
    $vagrant ssh node2
    
    vagrant@node2:~$ cqlsh 192.168.200.12
    Connected to Test Cluster at 192.168.200.12:9160.
    [cqlsh 4.1.0 | Cassandra 2.0.3 | CQL spec 3.1.1 | Thrift protocol 19.38.0]
    Use HELP for help.
    cqlsh>    
    

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/dholbrook/vagrant-cassandra/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

