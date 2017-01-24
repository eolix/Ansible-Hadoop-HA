# Ansible Hadoop HA
Original by [acorbacho@nflabs.com](mailto:acorbacho@nflabs.com) 
Modified by Patrik Ohlson - ZDi.it

# Ansible Hadoop
**Contributing:** [Contribution Guide](https://github.com/NFLabs/ansible-hadoop/blob/master/CONTRIBUTING.md)<br/>
**License:** [Apache 2.0](https://github.com/NFLabs/ansible-hadoop/blob/master/LICENSE)

Ansible Haddop is a playbook that help you to deploy a new Hadoop HA / Zookeeper cluster using Ansible.

The playbooks can:

 1. Deploy a fully functional Hadoop cluster **with High Availability (HA) and automatic failover**.
 2. Deploy additional nodes to scale the cluster

### List of services 
 * Hadoop
    * Zookeeper
    * Journalnode
    * HDFS

## Requirements
 * Ansible 1.6+
 * CentOS 7+ or RedHat servers

## Configuration

edit the files:

 * `hosts` : Set the hosts and services
 * `group_vars/all`: to change/add  more configuration parameters (ex: hdfs path, spark port etcetc) <br/>
 
  ```
  site_name: mycluster					# The name of your cluster
  update_iptables: True/False			# If True, change iptables file to add ip_range.
  update_hosts: True/False				# If True, set the hosts file to every host in the cluster.
  install_oracle_jdk: True/False		# If True, download and Install Oracle JDK from oracle server. 
  
  ```

# Deploy a new cluster

To run with Ansible:

```sh
./deploy
```

To e.g. just install ZooKeeper, add the `zookeeper` tag as argument.
available tags: 
 
 * hadoop
 * ntp
 * zookeeper
 * slaves

```sh
./deploy zookeeper
```

### Services url
Dont forget to open the port of the hosts if you want to access to your cluster remotely.


 * **HDFS : active**: master:50070 - *active*
 * **HDFS : stand by**: master2:50070 - *standby*

# Restart service or cluster

restart all services run 
```
./restart
```

If you want just restart some services run:

```sh
./restart serviceName
```

List of service that can be restarted

 * zookeepers
 * journalnodes
 * namenodes
 * datanodes


