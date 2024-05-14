# k8s-auto-provision


## Structure
![image](https://github.com/khoitranlord/k8s-auto-provision/assets/79269059/72845a79-a6f9-4211-95ed-af42638f3204)

In this case, proxy VM is reduced, we will run kubectl on ansible-control-node or k8s master-node:
Set up: 1 ansible control node,  1 k8s master node, 2 worker nodes.

Note: If VMs run on non-root user, add that current user to no-passworkd-requiered sudoers group with this commnad:
```
echo "$USER ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
```

## How to provison K8s cluster on remove VMs

### Install dependencies for VMs: 
Run:
```
ansible-playbook ~/ansible/playbooks/kube_dependencies.yml -i ~/ansible/inventory/kube_inventory
```
Note: Need to edit ~/ansible/inventory/kube_inventory for your configuration.

### Initialize cluster:
Run:
```
ansible-playbook ~/ansible/playbooks/kube_master.yml -i ~/ansible/inventory/kube_inventory
```

### Join worker nodes to cluster:
Run:
```
ansible-playbook ~/ansible/playbooks/kube_workers.yml -i ~/ansible/inventory/kube_inventory
```

### Test
Run command on master node:

```
kubectl get nodes
```
