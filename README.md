Take home test for DevOps/SysOps role – Level#2

1.	Create a Highly available Kubernetes cluster manually using Google Compute Engines (GCE). Do not create a Kubernetes hosted solution using Google Kubernetes Engine (GKE). Use Kubeadm(preferred)/kubespray. Do not use kops.

Followed the production installation in Kubernetes documentation and used kubespary to deploy
https://kubernetes.io/docs/setup/production-environment/tools/kubespray/

GCP Machine snapshot added File Name = GCP machine snapshot.png
On the Ansible host after setting up root ssh do the following

1.	Install EPEL release package
[root@ansible kubespray]# sudo yum install epel-release -y

2.	 Install pip
Once the EPEL repository is enabled we can install pip and all of its dependencies with the following command:
[root@ansible kubespray]# yum install python-pip -y

Check pip version

[root@ansible kubespray]# pip --version
pip 8.1.2 from /usr/lib/python2.7/site-packages (python 2.7)
[root@ansible kubespray]#

Development tools are required for building Python modules, you can install them with:
[root@ansible kubespray]# yum install python-devel -y
[root@ansible kubespray]# yum groupinstall 'development tools' -y

# Install dependencies from ``requirements.txt``
pip install -r requirements.txt


# Copy ``inventory/sample`` as ``inventory/mycluster ``
cp -rfp inventory/sample inventory/mycluster

After adjusting the inventory.ini file use the below command to install

[root@ansible kubespray]# ansible-playbook -e cloud_provider=gce -i /root/kubespray/inventory/mycluster/inventory.ini cluster.yml




After completion of installation below is the play recap
PLAY RECAP ***************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0
master1                    : ok=649  changed=128  unreachable=0    failed=0
master2                    : ok=557  changed=108  unreachable=0    failed=0
master3                    : ok=559  changed=109  unreachable=0    failed=0
node1                      : ok=419  changed=84   unreachable=0    failed=0
node2                      : ok=418  changed=84   unreachable=0    failed=0
node3                      : ok=418  changed=84   unreachable=0    failed=0

Friday 26 July 2019  07:24:29 +0000 (0:00:00.564)       0:36:23.676 ***********
===============================================================================
container-engine/docker : ensure docker packages are installed --------------------------------------------------- 71.88s
kubernetes/master : kubeadm | Init other uninitialized masters --------------------------------------------------- 58.74s
kubernetes/master : kubeadm | Initialize first master ------------------------------------------------------------ 36.50s
download : download | Download files / images -------------------------------------------------------------------- 25.61s
etcd : Gen_certs | Write etcd master certs ----------------------------------------------------------------------- 18.41s
download : download | Sync files / images from ansible host to nodes --------------------------------------------- 17.32s
kubernetes/preinstall : Install packages requirements ------------------------------------------------------------ 15.80s
download : download_container | Download image if required ------------------------------------------------------- 12.12s
download : download_container | Download image if required ------------------------------------------------------- 12.11s
download : download | Sync files / images from ansible host to nodes --------------------------------------------- 11.66s
etcd : reload etcd ----------------------------------------------------------------------------------------------- 11.57s
bootstrap-os : Install libselinux-python ------------------------------------------------------------------------- 11.52s
download : download | Sync files / images from ansible host to nodes --------------------------------------------- 11.47s
download : download | Download files / images -------------------------------------------------------------------- 11.03s
download : download | Download files / images -------------------------------------------------------------------- 10.76s
kubernetes-apps/ansible : Kubernetes Apps | Start Resources ------------------------------------------------------- 9.71s
download : download_container | Download image if required -------------------------------------------------------- 9.49s
download : download_container | Download image if required -------------------------------------------------------- 9.05s
download : download_container | Download image if required -------------------------------------------------------- 8.66s
download : download_container | Download image if required -------------------------------------------------------- 8.26s

Once Installation completes check the status and output is below 
Image added name is " HA-Cluster-Status.jpg" & "Ck=luster-info.jpg"


Remaining Part of this exercise is done in the local machine using Virtualbox due to cost factors in GCP or any other cloud provider. Formed a 3 node cluster (1-Mater and 2-Nodes)

2. Create a CI/CD pipeline using Jenkins (or a CI tool of your choice) outside Kubernetes cluster (not as a pod inside Kubernetes cluster).
Installed the Jenkin server and snapshots added in Jenkins folder. Could not tried CI/CD
3.	Create a development namespace.
Created development namespace using "kubectl create ns development" command and checked 
Guestbook application deployment screenshots are in development folder

4.	Deploy guest-book application (or any other application which you think is more suitable to showcase your ability, kindly justify why you have chosen a different application) in the development namespace.
Application deployed in the developement namespace and screenshot of gusetbook webpage attached in the 

5.	Install and configure Helm in Kubernetes
Helm installed and using Helm installed guestbook application in the default namespace, which is the 6th question.
All screenshots attached in the Helm folder

6.	Use Helm to deploy the application on Kubernetes Cluster from CI server. Also upgraded and rollback performed using helm

7.	Create a monitoring namespace in the cluster.
created a monitoring namespace using "kubectl create ns monitoring"

8.	Setup Prometheus (in monitoring namespace) for gathering host/container metrics along with health check status of the application. 
followed the below link to configure Prometheus
https://linuxacademy.com/blog/kubernetes/running-prometheus-on-kubernetes/

DashBoard Snaphost attached in Promrtheus folder

9.	Create a dashboard using Grafana to help visualize the Node/Container/API Server etc. metrices from Prometheus server. Optionally create a custom dashboard on Grafana

Grafana has been deployed following the below link 
https://docs.portworx.com/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/monitoring/monitoring-px-prometheusandgrafana.1/#installing-grafana

Screenshot attached in Grafana Folder

10.	Setup log analysis using Elasticsearch, Fluentd (or Filebeat), Kibana.
Not attempted

11.	Demonstrate Blue/Green and Canary deployment for the application (For e.g. Change the background color or font in the new version etc.,)
Installed an application called vote application with V3 & V4. 
Created the deployments in Parallel for v3 and v4 and tested both.
One using default service and another using adummy service.  
Then edited the service to point Green application using label selectors. 
Once Verified Green is working properly removed blue application to complete it.

12.	Write a wrapper script (or automation mechanism of your choice) which does all the steps above.
Not attempted as a wrapper kit for automation
