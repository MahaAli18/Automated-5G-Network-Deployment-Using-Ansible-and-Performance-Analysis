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
