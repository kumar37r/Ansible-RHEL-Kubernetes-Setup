# Bulding Kubernete Cluster 

This script is to setup Kubernetes Cluster on RHEL based operating systems using Ansible

1. Before running this script update hosts and group_vars/all files with your hostnames and IP addresses.
2. This script is suitable with 2 Controller nodes, 2 Worker nodes and 1 Load balancer node.
3. If you have more than these servers, you'll have to modify below configuration files
 /K8sHardWay/roles/Bootstrap_etcd_Cluster/templates/etcd.service 
 /K8sHardWay/roles/Bootstrap_Kube_Control/templates/kube-apiserver.service
 /K8sHardWay/roles/Provision_Generate_Certs/tasks/client_certs.yml
 /K8sHardWay/roles/Provision_Generate_Certs/tasks/k8s_api_certs.yml
 /K8sHardWay/roles/Provision_Generate_Certs/tasks/distribute_certs.yml
 /K8sHardWay/roles/Generating_Kubeconfigs/tasks/generate_kubeconfig.yml
 /K8sHardWay/roles/Generating_Kubeconfigs/tasks/distribute_config.yml
4. Run this before running ansible to support Password less SSH setup.
sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/g' /etc/ssh/sshd_config; echo "abcd1234" | passwd --stdin root; systemctl restart sshd; systemctl status sshd;
5. Information and supported links are provided in their respective role playbook files.
6. Ansible should be installed on the localhost where you are executing this playbook.
7. cd into K8sHardWay and run "ansible-playbook k8s_site.yml -i hosts" as root from your local machine.

Citations:
1. https://github.com/kelseyhightower/kubernetes-the-hard-way