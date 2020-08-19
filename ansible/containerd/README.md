# Kubernetes Cluster with Containerd
<p align="center">
<img src="https://kubernetes.io/images/favicon.png" width="50" height="50">
<img src="https://containerd.io/img/logos/icon/black/containerd-icon-black.png" width="50" >
</p>


This document provides the steps to bring up a Kubernetes cluster using ansible and kubeadm tools.

### Prerequisites:
- **OS**: SLES15sp2 and CentOS8.2
- **Python**: 2.7+
- **Ansible**: 2.4+

## Step 0:
-  Install Ansible on the host where you will provision the cluster. This host may be one of the nodes you plan to include in your cluster. Installation instructions for Ansible are found [here](http://docs.ansible.com/ansible/latest/intro_installation.html).
-  Create a hosts file and include the IP addresses of the hosts that need to be provisioned by Ansible.
```console
$ cat hosts
172.31.7.230
172.31.13.159
172.31.1.227
```
-  Setup passwordless SSH access from the host where you are running Ansible to all the hosts in the hosts file. The instructions can be found in [here](http://www.linuxproblem.org/art_9.html)

## Step 1:
At this point, the ansible playbook should be able to ssh into the machines in the hosts file.
```console
git clone https://github.com/jbsparks/c9s.git
cd c9s/ansible/containerd
ansible-playbook -i hosts cri-containerd.yaml
```
### Important files

* __var/vars.yaml__ specifies the version of containered


For more options ansible config file (/etc/ansible/ansible.cfg) can be used to set defaults. Please refer to [Ansible options](http://docs.ansible.com/ansible/latest/intro_configuration.html) for advanced ansible configurations.

At the end of this step, you will have the required software installed in the hosts to bringup a kubernetes cluster.
```console
PLAY RECAP ***************************************************************************************************************************************************************
172.31.1.227               : ok=21   changed=7    unreachable=0    failed=0
172.31.13.159              : ok=21   changed=7    unreachable=0    failed=0
172.31.7.230               : ok=21   changed=7    unreachable=0    failed=0
```
