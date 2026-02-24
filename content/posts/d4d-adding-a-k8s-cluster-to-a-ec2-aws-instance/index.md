---
id: "Xngi4dcUTcm27mUUL4CFIQ"
status: "published"
createdAt: "2024-09-06T16:45:09+01:00"
firstPublishedAt: "2024-09-06T16:45:12+01:00"
publishedAt: "2024-09-06T16:45:12+01:00"
updatedAt: "2024-09-06T16:45:09+01:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/growtika-zfvyuv8l7wu-unsplash.jpg"
date: "2024-09-09"
excerpt: "Step by Step guide to build a K8s cluster in a EC2 AWS instance"
slug: "d4d-adding-a-k8s-cluster-to-a-ec2-aws-instance"
title: "D4D - Adding a K8s cluster to a EC2 AWS instance"
---

# D4D - Adding a K8s cluster to a EC2 AWS instance

# Introduction

> This post assumes you have an AWS EC2 instance running. For more information, refer to this post: on https://blog.vicensfayos.consulting/posts/create-configure-access-ec2-instance-using-aws-cli
>
>

Now that we have our running EC2 instance is time to install Kubernetes on it. 

Installing Kubernetes packages does not differ too much from installing any other service in a linux server.

I will not be very specific in the details as you can use google and any LLM to get more specific details. For me the important thing of all this series of posts if that you follow me in the path to set and use CI/CD properly

But before print the commands themself let's briefly discuss the architecture. 

We want to create and configure a K8S Cluster. By definition a K8S cluster is made from several nodes and, as a good practice, tends to be a virtual machine on his own. 

Nodes divides themself in 2 kinds. One the Master or Control Plane node is the one responsible to manage, provision and schedule the other nodes, the worker nodes. Those nodes contain the applications that we want to deploy and publish out there. 

Therefore, after all said above, a common architecture of nodes is having a VM with a control plane node and 1 or more virtual machines as a worker nodes. 

But for our learning process we will just keep working in a single Virtual Machine and the Node that acts as Control Plane node will act also as Worker Node. 

Why to do that? To save money basically. Joining nodes in a cluster is not time consuming and I will explain you also what to do in case you prefer a more "production ready" approach. 

# \# Install all needed packages

Below all commands you need to run in your EC2 to have needed K8S packages ready to be used 

## Prerrequisites

```bash
## Update system packages
sudo apt update && sudo apt upgrade -y

## Disable Swap (required by Kubernetes):
sudo swapoff -a 
sudo sed -i '/swap/d' /etc/fstab

## Load Kernel Modules and Configure sysctl for Kubernetes:

cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf 
br_netfilter overlay 
EOF 

sudo modprobe br_netfilter 
sudo modprobe overlay 

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf net.bridge.bridge-nf-call-iptables = 1 net.bridge.bridge-nf-call-ip6tables = 1 net.ipv4.ip_forward = 1 
EOF
```

## Installing all K8s packages

```bash
# For each Node you want to have (VM) run the following commmands
# I used a EC2 Ubuntun 22.4 instance. 

sudo apt-get install -y containerd

#Install Kubernetes packages - kubeadm, kubelet and kubectl

#Add Google's apt repository gpg key

sudo apt-get install -y apt-transport-https ca-certificates curl gpg

sudo curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# Add the Kubernetes apt repository
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

# install required packages pay attention to set a version if you dont want to install the lastest one 
VERSION=1.30.4-1.1 # in my case
sudo apt-get install -y kubelet=$VERSION kubeadm=$VERSION kubectl=$VERSION

# prevent packages are automatically updated
sudo apt-mark hold kubelet kubeadm kubectl containerd
```

## Check that everything is on place

Some useful commands to see if installation was succesful

```bash
kubectl get pods --all-namespaces
kubectl get nodes
sudo systemctl status kubelet.service
```

## Create the cluster

Once you have all the packages you need, you can proceed to install the cluster.

```bash
# Install a Pod netwoking tool, I use calico
wget https://raw.githubusercontent.com/projectcalico/calico/master/manifests/calico.yaml

# Create the Cluster itsef
sudo kubeadm init --kubernetes-version $VERSION

## After init was succesful and following prompt instructions do this
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Apply the Calico yml you downloaded
kubectl apply -f calico.yaml
```

## Make Control Plane act as a Node

As commented about, we want to have just a VM with a Node that works as a master and as worker, for achieving that you need to do the following: 

```bash
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

With this you say that the control plane node can also take care of scheduling normal Nodes

# Bonus: having Control Node and Worked Node\(s\) with several VM

If you want to go for the most professional \(and expensive\) version, and pay more you need to do the following



- Install the needed packages in each of the VM you want to have a Worker \(See: Install all needed packages section\)
- Go to the Control Plane VM and run this command:

```bash
kubeadm token create --print-join-command
```

Something similar to this will be print:

```bash
sudo kubeadm join <your_control_plane_ip>:6443 \
--token a2345.wprtltpo234240 \
--discovery-token-ca-cert-hash sha256:skdufghskrywi3uyeti734ty2i374y238i47y623iwieruyeirugwer
```

Grab this command and, for each worker run in in a console \(you have to connect by SSH\).

As a result, you will have as output a confirmation that the Worker Node joined the Control Plane Node and if you run `kubectl get nodes`  in the control plane VM / node you will se more than one node listed, the control plane one and N nodes as you have joined. 

# Summary

This is all, now we have a ready to go K8S installation in VM EC2 server in AWS.

We can now start with the CD itself using containers and Kubernetes! 

See you in next posts!!
