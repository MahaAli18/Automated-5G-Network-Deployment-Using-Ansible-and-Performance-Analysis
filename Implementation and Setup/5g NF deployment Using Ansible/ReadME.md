# 5G Core Network Functions, UE, and eNB deployment using Ansible automation tool:


To simplify 5G deployment, the project is intended to automate the installation of the 5G non-standalone network. 5G automation improves operational efficiency, lessens the time to market for new services, lowers total cost, reduces network operations and service management errors, and speeds up processes. In this project, we will be automating the deployment of Network Functions (NFs) that are part of the 5g system architecture, such as PCRF, HSS, SMF, and UPF, along with the user equipment (UE’s) and eNodeB (eNB). To ensure that the 5g deployment works seamlessly in any environment, docker containers will be utilized to package our core network functions, UE’s, an eNB, and all their dependencies together in containers. Moreover, the containers don't require the entire OS, consume fewer hardware resources, have shorter Startup times, require less maintenance, and are very portable. We deploy locally on Ubuntu 20.04 LTS, with 4GB RAM and 100GB disk space. We're employing an ansible playbook for automation since it's a blueprint of automation tasks. The playbook code is written in human-readable YAML format that includes the hostname, classes, and tasks required for automating the deployment of the 5g Network. For deploying a 5g network through an automation tool ansible on your system, follow the mentioned steps in the given order.
System Requirements:
·   	Ubuntu Version: 20.04 LTS
·   	Disk Space: 100 GB
·   	RAM: 4 GB
