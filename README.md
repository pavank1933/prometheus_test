# prometheus_test
Prometheus configuration using Ansible &nbsp;
Prometheus -> Written in Golang &nbsp;
It records time series data &nbsp;

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
 
 
 
***********Prometheus POC*********** {Monitor itself poc}&nbsp;
https://prometheus.io/docs/prometheus/latest/getting_started/  &nbsp;
 
********GRAFANA POC***********&nbsp;
https://prometheus.io/docs/visualization/grafana/&nbsp;

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

*************Install, configure and monitor our first resource with Prometheus*************{start this for poc}&nbsp;
https://prometheus.io/docs/introduction/first_steps/&nbsp;

*****Install Prometheus**** &nbsp;
wget https://github.com/prometheus/prometheus/releases/download/v2.2.0/prometheus-2.2.0.linux-amd64.tar.gz  &nbsp;
tar xvfz prometheus-*.tar.gz  &nbsp;
cd prometheus-*    &nbsp;
cp -rpf prometheus.yml  prometheus.yml-orig   &nbsp;
./prometheus --config.file=prometheus.yml   &nbsp;


*****Installing the Node Exporter****  &nbsp;
yum update -y   &nbsp;
wget https://github.com/prometheus/node_exporter/releases/download/v0.16.0-rc.0/node_exporter-0.16.0-rc.0.linux-amd64.tar.gz   &nbsp;
tar xvfz node_exporter-*.tar.gz  &nbsp;
cd node_exporter-* &nbsp;

./node_exporter     &nbsp;


*******Prometheus reload configuration info*******    &nbsp;
https://www.robustperception.io/reloading-prometheus-configuration/    &nbsp;

******Stop prometheus server******   &nbsp;
ctrl+c to stop prometheus server    &nbsp;

********to test whether we can ping target metrics from prometheus server****** &nbsp;
curl -v -o /dev/null http://107.20.11.87:9100/metrics   &nbsp;
