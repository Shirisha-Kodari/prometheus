## create prometheus server
# step-1: login ti server and install prometheus in server 
create one directory cd /opt/ 
install with root access sudo su - 
wget  https://github.com/prometheus/prometheus/releases/download/v3.9.0-rc.0/prometheus-3.9.0-rc.0.linux-amd64.tar.gz 

# step-2: Extract prometheus file 
tar -xf  prometheus-3.9.0-rc.0.linux-amd64.tar.gz

# Rename prometheus :
mv prometheus-3.9.0-rc.0.linux-amd64 prometheus
# step-3: create prometheus service filr 
sudo vim /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus Service
After=network.target

[Service]
ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml
Restart=on-failure

[Install]
WantedBy=multi-user.target

# step-4:
* after changes in config file or service file 
* systemctl daemon-reload
* systemctl restart prometheus 
port:9090
# node-1 server creation 
* install node_exporter
https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz

 tar -xf node_exporter-1.10.2.linux-amd64.tar.gz
mv node_exporter-1.10.2.linux-amd64 node_exporter
# create service
sudo vim /etc/system/system/node_exporter

[Unit]
Description=Node Exporter Service
After=network.target

[Service]
ExecStart=/opt/node_exporter/node_exporter
Restart=on-failure

[Install]
WantedBy=multi-user.target

systemctl daemon-reload
systemctl restart node_exporter
port :9100
# grafana configuration 
*create grafana server and install grafana on server 
wget -q -O gpg.key https://rpm.grafana.com/gpg.key or curl -o gpg.key https://rpm.grafana.com/gpg.key

sudo rpm --import gpg.key

/etc/yum.repos.d/grafana.repo 

[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt

sudo dnf install grafana

 systemctl daemon-reload

systemctl restart grafana-server 

connected to garfana ui 
grafana public ip :3000

 