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
  