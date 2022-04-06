# Monitoring 5G docker containers that were earlier deployed through ansible:

Container monitoring aids operations teams in identifying and resolving underlying issues in a timely manner. Basic data such as CPU usage, memory utilization, container size, and bandwidth utilization, to name a few, are captured as part of container monitoring. We can also collect real-time logs, which are useful for debugging and alerting the IT staff when it’s time to scale up. In this section, we have used the enhanced Zabbix agent i.e.zabbix agent 2, which will fetch the performance metrics from the remote host where the docker containers are deployed. This agent will communicate the metric data to the Zabbix server which is deployed on the other virtual machine.

Zabbix agent 2 is a new generation of Zabbix agents and may be used in place of the Zabbix agents. 
### Zabbix agent 2 has been developed to:
* reduce the number of TCP connections
* provide improved concurrency of checks
* be easily extendible with plugins. A plugin should be able to:
* provide trivial checks consisting of only a few simple lines of code
* provide complex checks consisting of long-running scripts and standalone data gathering with periodic sending back of the data
* be a drop-in replacement for Zabbix agent (in that it supports all the previous functionality)

Zabbix agent 2 will be beneficial for 5G based environment as by default,Zabbix agent 2 schedules the first data collection for active checks at a conditionally random time, which is less than item update interval, to prevent spikes in resource usage and better performance monitoring.

### Configuration on :
Ubuntu 20.4 ( The same VM on which the 5G docker containers are deployed ) and SSH access to this server node with a sudo user already configured )

### Step 1:
To monitor the 5G network containers , first the zabbix repository is installed and zabbix agent 2 is deployed upon the remote host i.e. our docker server , where the containers are deployed.

```sudo wget https://repo.zabbix.com/5.4/ubuntu/pool/main/z/zabbix-release/zabbix-release-5.4-1+ubuntu20.04-all.deb```

```sudo dpkg -i zabbix-release-5.4-1+ubuntu20.04-all.deb```

```sudo apt update```

```sudo apt install zabbix-agent2```

### Step 2:

The Zabbix agent is configured by default to send metrics to the Zabbix server on the same host where it is installed. Some additional variables are required because our goal is to monitor docker containers on a distant host.

```sudo vim /etc/zabbix/zabbix-agent2.conf```

Following configurations are done in the zabbix agent 2 config file :

```Server: 192.168.64.6 ( zabbix server IP )```

```ServerActive: 192.168.64.6 ( zabbix server IP )```

```Hostname : maha-virtual-machine ( our docker container server )```

### Step 3:
Zabbix user is added, which is installed by default, to the docker group for the Zabbix agent to monitor Docker containers.


```sudo usermod -aG docker zabbix```

### Step 4:
Apply all the changes and enable the zabbix agent 2

```sudo systemctl restart zabbix-agent2```

```sudo systemctl enable zabbix-agent2```

### Step 5:
Running the status command to see zabbix agent 2 is running or not

``` sudo systemctl status zabbix-agent2```

### Step 6:
Now moving to the browser from 
```https//:192.168.64.6/zabbix```
and then configuring a zabbix host in order to monitor the 5G deployed containers.

![This is an image](https://github.com/MahaAli18/Automated-5G-Network-Deployment-Using-Ansible-and-Performance-Analysis/blob/main/Implementation%20and%20Setup/images/Host%20Configuration.png)

### Step 7: 
Creating a host at zabbix frontend and adding a template called "Template app docker". This is the template for all the parameters of docker which are to be shared.
![This is an image](https://github.com/MahaAli18/Automated-5G-Network-Deployment-Using-Ansible-and-Performance-Analysis/blob/main/Implementation%20and%20Setup/images/Connection%20success%20ZBX%20green.png)
![This is an image](https://github.com/MahaAli18/Automated-5G-Network-Deployment-Using-Ansible-and-Performance-Analysis/blob/main/Implementation%20and%20Setup/images/Template%20App%20docker.png)
![This is an image](https://github.com/MahaAli18/Automated-5G-Network-Deployment-Using-Ansible-and-Performance-Analysis/blob/main/Implementation%20and%20Setup/images/container%20integration.png)
