# 5G network monitoring using Zabbix tool


Once the 5G network functions are deployed through docker and Kubernetes with the use of ansible , the next major step for any network provider is to monitor the networks and further be proactively prepared for any circumstances of disaster recovery. It is well known that proactive actions by the operations department of any network providing organisation has always yield a major advantage in saving the downtime costs and further for maintaining the integrity towards the valued customers.Keeping this crucial part of network monitoring in automated network deployment as a priority , this report lists the most suitable and efficient way of monitoring the 5G network. We propose a solution to monitoring withthe help of Zabbix Tool which is an open-source software tool to monitor IT infrastructure such as networks, servers, virtual machines, and cloud services.

Zabbix architecture consists of the Zabbix server and Zabbix agent and it employs a client-server architecture, with an agent installed on the servers to be monitored. This agent collects and communicates all necessary information and status from the system to the Zabbix server.

5G networks with the distributed edge functionality , gives rise to many open ended solutions which can be followed while minimizing the downtime and this can be regulated by the time in which the performance metrics from the monitoring tool are fetched and then further analyzed. This can be achieved by modulating the client-server model of Zabbix and analyzing that which configuration suits best for the robustness of the 5G deployment.
Further insights to this are provided in the future works column of this report.

This project aims at the integration part of zabbix with the web based GUI installation and aligning the local VM for the monitoring first and then monitoring the 5G network functions deployed docker containers.
