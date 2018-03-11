# prometheus_test   

What is prometheus?
Prometheus is a systems and services monitoring system. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts if some condition is observed to be true.
Prometheus' main distinguishing features as compared to other monitoring systems are:
 * A multi-dimensional data model (timeseries defined by metric name and set
   of key/value dimensions).
 * A flexible query language to leverage this dimensionality.
 * No dependency on distributed storage; single server nodes are autonomous.
 * Timeseries collection happens via a pull model over HTTP.
 * Pushing timeseries is supported via an intermediary gateway.
 * Targets are discovered via service discovery or static configuration.
 * Multiple modes of graphing and dashboarding support.
 * Federation support coming soon.


Prometheus configuration using Ansible    <br/>
Prometheus -> Written in Golang   <br/>
It records time series data    <br/>
 
***********Prometheus POC*********** {Monitor itself poc}    <br/>
https://prometheus.io/docs/prometheus/latest/getting_started/    <br/>
 
********GRAFANA POC***********    <br/>
https://prometheus.io/docs/visualization/grafana/  <br/>


*************Install, configure and monitor our first resource with Prometheus*************{start this for poc}  <br/>
  https://prometheus.io/docs/introduction/first_steps/   <br/>

*****Install Prometheus****   <br/>
wget https://github.com/prometheus/prometheus/releases/download/v2.2.0/prometheus-2.2.0.linux-amd64.tar.gz    <br/>
tar xvfz prometheus-*.tar.gz   <br/>
cd prometheus-*    <br/>
cp -rpf prometheus.yml  prometheus.yml-orig     <br/>
./prometheus --config.file=prometheus.yml   <br/>


*****Installing the Node Exporter****   <br/>
yum update -y   <br/>
wget https://github.com/prometheus/node_exporter/releases/download/v0.16.0-rc.0/node_exporter-0.16.0-rc.0.linux-amd64.tar.gz    <br/>
tar xvfz node_exporter-*.tar.gz   <br/>
cd node_exporter-* <br/>

**********To start node exporter service************<br/>
./node_exporter     <br/>


*******Prometheus reload configuration info*******    <br/>
https://www.robustperception.io/reloading-prometheus-configuration/    <br/>

******Stop prometheus server******    <br/>
ctrl+c to stop prometheus server     <br/>

********To test whether we can ping target metrics from prometheus server******   <br/>
curl -v -o /dev/null http://107.20.11.87:9100/metrics     <br/>
  
  
*****************************Ansible************************************   <br/>
*****To execute playbooks on localhost use the below command*****  <br/>
ansible-playbook -i "localhost," -c local test.yml <br/>

******change the hosts file with{Its a remote server} ********* <br/>
[webservers] <br/>
54.*.*.*  

ansible-playbook -i /etc/ansible/hosts test.yml <br/>

export ANSIBLE_HOST_KEY_CHECKING=False  <br/>
*****Do this when host key verification failed********	  <br/>	 


**********To execute playbook on the remote server*************	  <br/>	 
$ ansible-playbook -i /etc/ansible/hosts test.yml -vvvv   <br/>

In the above command /etc/ansible/hosts file consists of remote amazon linux server. Playbook "test.yml" file <br/> 
constains postgres client to get installed on the remomte server. For this we need to do put ssh keys in the  <br/>
remote host. <br/>
*Do the below procedure:-  <br/>

Lets say you have 2 machines. Machine A {Ansible Host} & Machine B{ target}<br/>

On the Machine A, you will have to generate a sshkey using : <br/>

~$ ssh-keygen   <br/>
This will generate a Public and Private key pair in .ssh directory of your current user. <br/>

Once the keys are generated you need to copy the public key {extension .pub}{/root/.ssh/id_rsa.pub} from the  <br/>
Machine A's .ssh directory.  <br/>

Now Login to Machine B , and go inside .ssh folder of it. <br/>
Now you need to create a file called "authorized_keys" (if not present, make sure the permission is readonly)  <br/>
and paste the copied public key from Machine A to machine B. <br/>

This is done . <br/>

Now in your host{inventory} file on machine A use the following format :  <br/>

[hosts]   <br/>
Machine_B_ip ansible_ssh_user=username_here ansible_ssh_private_key_file=/path_of_private_key    <br/>

In the /etc/ansible/hosts paste the below code:-    <br/>		 

[webservers]     <br/>
54.*.*.*  ansible_ssh_user=ec2-user  ansible_ssh_private_key_file=/root/.ssh/id_rsa      <br/>
Note:-   <br/>
54.*.*.* is the remote server.    <br/>
ansible_ssh_user=ec2-user    #Remote server user    <br/>
ansible_ssh_private_key_file=/root/.ssh/id_rsa      #Machine A private key file   <br/>

		 
Now run the below command:-     <br/>
ansible-playbook -i /etc/ansible/hosts test.yml -vvvv           <br/>
Note:- This playbook installs postgres client on remote server using hosts file	  <br/>	 
