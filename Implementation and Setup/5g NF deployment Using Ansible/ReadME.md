# 5G Core Network Functions, UE, and eNB deployment using Ansible automation tool:


To simplify 5G deployment, the project is intended to automate the installation of the 5G non-standalone network. 5G automation improves operational efficiency, lessens the time to market for new services, lowers total cost, reduces network operations and service management errors, and speeds up processes. In this project, we will be automating the deployment of Network Functions (NFs) that are part of the 5g system architecture, such as PCRF, HSS, SMF, and UPF, along with the user equipment (UE’s) and eNodeB (eNB). To ensure that the 5g deployment works seamlessly in any environment, docker containers will be utilized to package our core network functions, UE’s, an eNB, and all their dependencies together in containers. Moreover, the containers don't require the entire OS, consume fewer hardware resources, have shorter Startup times, require less maintenance, and are very portable. We deploy locally on Ubuntu 20.04 LTS, with 4GB RAM and 100GB disk space. We're employing an ansible playbook for automation since it's a blueprint of automation tasks. The playbook code is written in human-readable YAML format that includes the hostname, classes, and tasks required for automating the deployment of the 5g Network. For deploying a 5g network through an automation tool ansible on your system, follow the mentioned steps in the given order.
System Requirements:
*   Ubuntu Version: 20.04 LTS
* 	Disk Space: 100 GB
*  	RAM: 4 GB
## Implementation Steps:

### Step 1: Docker Installation and Setup 

Uninstall old versions:

``` sudo apt-get remove docker docker-engine docker.io containerd runc ```

Set up the repository:

```sudo apt-get update```

```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```    

```
sudo apt-get update
sudo apt-get install \ca-certificates \ curl \ gnupg \ lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo\"deb[arch=$(dpkg--print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

```

![This is an image](/Automated-5G-Network-Deployment-Using-Ansible-and-Performance-Analysis/Implementation_and_Setup/images/docker_setup.png)


### Step 2: Clone Free5gc:
```
sudo git clone https://github.com/free5gc/free5gc.wiki.git
 ```
 
 ### Step 3: Create Network using the Docker command
```
docker network create -d bridge my-bridge-network
ifconfig
```

### Step 4: Run ansible-playbook code:

The architecture will be deployed using Playbook code, and users will only need to run one command to have a 5G network functioning locally or in the cloud. Clone and change it per system specifications and save the file in YAML format.

```
sudo ansible-playbook -K file_name.yml -e "internet_network_interface=<< internet_network_interface >>"

```
### Step 5: To Check the Status of Containers running.
```
sudo docker ps

```
### Step 6: Test and access UE’s components
```docker exec -ti ue bash```

```ping labora.inf.ufg.br -I «ip-address-user-equipment-interface»```

## Orchestrating containers using Kubernetes:
To illustrate and monitor functions of the 5G deployment in the cloud, Kubernetes is used to orchestrate all the containerized components of the 5G network like core network functions, UE, and gNodeB. Kubernetes is an open-source framework for managing containerized workloads and services that enables declarative configuration and automation. It has a vast and fast-expanding ecosystem. Kubernetes' automation makes developing container-based apps much more accessible.

### System Requirements:
Ubuntu Version: 18.04.6 LTS (Bionic Beaver)
Disk Space: 100 GB
RAM: 4 GB

### Step 1: Kubernetes Installation and Setup
```
sudo apt-get update
sudo apt-get install curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get install kubeadm kubelet kubectl kubernetes-cni
sudo swapoff -a
sudo kubeadm init
```
### Step 2: Setting up the local Kubernetes Cluster using minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
sudo -E minikube start --driver=none
sudo minikube start
```
### Step 3: Setting up the Kubectl
```
sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2 curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
sudo kubectl create -f https://raw.githubusercontent.com/openshift/etcd-ha-operator/master/deploy/rbac.yaml
sudo kubectl create -f https://raw.githubusercontent.com/openshift/etcd-ha-operator/master/deploy/crd.yaml
sudo kubectl create -f https://raw.githubusercontent.com/openshift/etcd-ha-operator/master/deploy/restore_crd.yaml
sudo kubectl create -f https://raw.githubusercontent.com/openshift/etcd-ha-operator/master/deploy/backup_crd.yaml
sudo kubectl create -f https://raw.githubusercontent.com/openshift/etcd-ha-operator/master/deploy/operator.yaml
sudo kubectl create -f https://raw.githubusercontent.com/openshift/etcd-ha-operator/master/deploy/cr.yaml
sudo kubectl get pods
```

### Step 4: Deploying images from Free5gc and setting up AMF/UPF

Images are pulled from the free5gc. The images can be found on the link.
```
sudo kubectl apply -f unix-daemonset.yaml
sudo kubectl apply -f free5gc-mongodb.yaml
sudo kubectl apply -f free5gc-configmap.yaml
sudo kubectl apply -f free5gc-nrf.yaml
sudo kubectl apply -f free5gc-ausf.yaml
sudo kubectl apply -f free5gc-smf.yaml
sudo kubectl apply -f free5gc-nssf.yaml
sudo kubectl apply -f free5gc-pcf.yaml
sudo kubectl apply -f free5gc-udm.yaml
sudo kubectl apply -f free5gc-udr.yaml
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o ens4 -j MASQUERADE
git clone https://github.com/PrinzOwO/gtp5g
cd gtp5g
sudo apt install make
```
