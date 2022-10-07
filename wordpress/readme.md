 * Copyright 2021-2022 Cloud Side Company 
 * All Rights Reserved. Confidential and Proprietary.
 * For more information, please contact:
 * Cloud Side Company, Montemiletto, Avellino, IT

# Wiki Deploy Wordpress on your k3s Rancher deployment

## Deploy wordpress stateless

## Prerequisites

 * A running cluster k3s with rancher 2.6

#### Create Deployment sample

Create deployment from Cluster/workloads/deployments.

    Image: rancher/hello-world:latest
    Service NodePort (80)

### Deploy Wordpress

Create namespace 'stateless-wordpress'

dfd
