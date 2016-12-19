Scale-out Load-Balancer Demo
===========================

This demo shows a topology using 'Routing on the Host' to add host reachability directly into a BGP routed fabric. Switches are Cumulus Linux and servers running Ubuntu. This playbook configures a CLOS topology running BGP unnumbered in the fabric with numbered links towards the hosts. 

The Ubuntu server acts as the host to redistribute kernel routes as /32 host routes into the routing table when VMs or containers become available. When the demo runs successfully, any server on the network should be able to access the webserver via the BGP routes established over the fabric.

NGINX is installed on server01-04. Server01 and Server03 are configured as a front end LB tier, Server02 and server04 are confifgured as standard webservers.

The purpose of this demo is to experiment with session sharing between LBs and see the impact in an ECMP L3 fabric with anycast service IPs (aka V-IPs).

This demo is written for the [cldemo-vagrant](https://github.com/cumulusnetworks/cldemo-vagrant) reference topology and applies the reference BGP unnumbered configuration from [cldemo-config-routing](https://github.com/cumulusnetworks/cldemo-config-routing).


Quickstart: Run the demo
------------------------
Before running this demo, install [VirtualBox](https://www.virtualbox.org/wiki/Download_Old_Builds) and [Vagrant](https://releases.hashicorp.com/vagrant/). The currently supported versions of VirtualBox and Vagrant can be found on the [cldemo-vagrant](https://github.com/cumulusnetworks/cldemo-vagrant).

    ### Bring up the vagrant topology
    git clone https://github.com/cumulusnetworks/cldemo-vagrant
    cd cldemo-vagrant
    vagrant up oob-mgmt-server oob-mgmt-switch leaf01 leaf02 spine01 spine02 server01 server02

    ### setup oob mgmt server
    vagrant ssh oob-mgmt-server
    sudo su - cumulus
    sudo apt-get install software-properties-common -y
    sudo apt-add-repository ppa:ansible/ansible -y
    sudo apt-get update
    sudo apt-get install ansible -qy

    ### Run the ROH demo
    git clone https://github.com/cnidus/cldemo-lb-ansible
    cd cldemo-lb-ansible
    ansible-playbook run-demo.yml

    ### Something will go here eventually...
