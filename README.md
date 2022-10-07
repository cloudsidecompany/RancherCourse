 * Copyright 2021-2022 Cloud Side Company 
 * All Rights Reserved. Confidential and Proprietary.
 * For more information, please contact:
 * Cloud Side Company, Montemiletto, Avellino, IT

# Wiki Deploy Rancher on your Linux Machine with k3s

## Deploy Rancher on Linux CentOS/RHEL from version 8.0

## Prerequisites

 * Install [Docker](https://docs.docker.com/engine/install/centos/) and make your user in [Sudoers](https://docs.docker.com/engine/install/linux-postinstall/).
 * Install [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) official.
 * Install [Helm](https://helm.sh/docs/intro/install/) official.
 * Make sure the docker images repositories are accessible for the cluster.

## Installing 

### Rancher on K3s distribution

#### Install k3s from script.

    curl -sfL https://get.k3s.io | sh -s - server --cluster-init

#### Save the kubeconfig to your workstation

    mkdir ~/.kube
    sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
  
#### Edit the Rancher server URL in the kubeconfig

    vi ~/.kube/config

#### Install Rancher with Helm

    helm repo add rancher-latest https://releases.rancher.com/server-charts/latest

    kubectl create namespace cattle-system
    
    kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.7.1/cert-manager.crds.yaml

    helm repo add jetstack https://charts.jetstack.io
    
    helm repo update
    
    helm install cert-manager jetstack/cert-manager \
    --namespace cert-manager \
    --create-namespace \
    --version v1.7.1
    
    helm install rancher rancher-latest/rancher \
    --namespace cattle-system \
    --set hostname=<IP_OF_LINUX_NODE>.sslip.io \
    --set replicas=1 \
    --set bootstrapPassword=<PASSWORD_FOR_RANCHER_ADMIN>

 * Wait some minutes for rancher goes up.

Go to the chosen host (es. rancher.example.sslip.io) and follow the instructions displayed in the browser. \
Note: Make sure you have entered the ip/domain match in the hosts file of the machine you want to access from. \
Eg: `192.168.1.24 rancher.example.sslip.io`.
