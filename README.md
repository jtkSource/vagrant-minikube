
# Vagrantfile and Scripts to Automate Minikube Setup

## Documentation

## Prerequisites

- Working Vagrant setup
- 4 Gig  RAM and 2 CPU workstation

## For Linux Users

Latest version of Virtualbox for Linux can cause issues because you have to create/edit the /etc/vbox/networks.conf file and add:
<pre>* 0.0.0.0/0 ::/0</pre>

or run below commands

```shell
sudo mkdir -p /etc/vbox/
echo "* 0.0.0.0/0 ::/0" | sudo tee -a /etc/vbox/networks.conf
```

So that the host only networks can be in any range, not just 192.168.56.0/21 as described here:
https://discuss.hashicorp.com/t/vagrant-2-2-18-osx-11-6-cannot-create-private-network/30984/23


## Create VM

Change Directory to project folder and run 

```
cd vagrant-minikube
vagrant up

```

## First time configure 

Start minikube the firsttime to download minikube

```shell

vagrant ssh minikube

vagrant@minikube-node:~$ sudo usermod -aG docker $USER

vagrant@minikube-node:~$ newgrp docker

vagrant@minikube-node:~$ minikube start --vm-driver=docker

vagrant@minikube-node:~$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

```

Update bash to include 

```
vi ~/.bashrc
source <(kubectl completion bash)
alias k=kubectl
complete -F __start_kubectl k

```
(Need to logout and login for bash completion to take effect)

## Stop Minikube 
```
minikube stop
```

## To shutdown the cluster,

```shell
vagrant halt
```

## To restart the cluster,

```shell
vagrant up

```
### Start Minikube

- Login to minikube with vagarant `vagrant ssh minikube`
- Start minikube with `minikube start`
- Check status with `minikube status` 


## To destroy the cluster,

```shell
vagrant destroy -f
```