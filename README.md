# prometheus_test   
Prometheus configuration using Ansible    <br/>
Prometheus -> Written in Golang   <br/>
It records time series data    <br/>

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
 
 
 
***********Prometheus POC*********** {Monitor itself poc}
https://prometheus.io/docs/prometheus/latest/getting_started/  
 
********GRAFANA POC***********
https://prometheus.io/docs/visualization/grafana/












*************Install, configure and monitor our first resource with Prometheus*************{start this for poc}
https://prometheus.io/docs/introduction/first_steps/

*****Install Prometheus**** 
wget https://github.com/prometheus/prometheus/releases/download/v2.2.0/prometheus-2.2.0.linux-amd64.tar.gz  
tar xvfz prometheus-*.tar.gz  
cd prometheus-*    
cp -rpf prometheus.yml  prometheus.yml-orig   
./prometheus --config.file=prometheus.yml   


*****Installing the Node Exporter****  
yum update -y   
wget https://github.com/prometheus/node_exporter/releases/download/v0.16.0-rc.0/node_exporter-0.16.0-rc.0.linux-amd64.tar.gz   
tar xvfz node_exporter-*.tar.gz  
cd node_exporter-* 

./node_exporter     


*******Prometheus reload configuration info*******    
https://www.robustperception.io/reloading-prometheus-configuration/    

******Stop prometheus server******   
ctrl+c to stop prometheus server    

********to test whether we can ping target metrics from prometheus server****** 
curl -v -o /dev/null http://107.20.11.87:9100/metrics   
