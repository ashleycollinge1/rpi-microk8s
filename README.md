# Raspberry Pi MicroK8s cluster deployment

I wanted to set up a small Kubernetes cluster on a few Raspberry Pis I have lying around. This repo contains the Ansible playbooks and my inventory for my deployment, you can modify as required.

## Guidance

### Prepare Raspberry Pis

1. Set hostname
2. Generate SSH keys and copy to management laptop

### Run Ansible

1. Run node-prep.yml on Inventory to prepare the nodes.
```
ansible-playbook -I ~/github.com/ashleycollinge1/rpi-microk8s/Inventory/microk8s.yml \
                 ~/github.com/ashleycollinge1/rpi-microk8s/Playbooks/node-prep.yml
```

2. Run cluster-deploy.yml on Inventory to install MicroK8s cluster on RPis.
```
ansible-playbook -I ~/github.com/ashleycollinge1/rpi-microk8s/Inventory/microk8s.yml \
                 ~/github.com/ashleycollinge1/rpi-microk8s/Playbooks/cluster-deploy.yml
```

## Inventory

* Define all of the Raspberry Pis, including defining the master node.

## Playbooks

* Prepare Rasbperry Pis
  * Confirms hostname, IP is set.
  * Creates aliases in /etc/hosts so each Rasberry Pi can talk to each other using DNS.
  * Create firewall rules for MicroK8s
* Deploy-MicroK8s
  * Sets up the master node
  * Goes to the other Raspberry Pis and add them to the cluster