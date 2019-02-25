# systemd
---

1. cd /usr/lib/systemd/system
2. vi etcd.service
    ```yaml
    [Unit]
    Description=Etcd Server
    After=network.target
    After=network-online.target
    Wants=network-online.target

    [Service]
    Type=notify
    WorkingDirectory=/opt/bin/
    # User=etcd
    ExecStart=/opt/bin/etcd --config-file=/etc/etcd/etcd.conf
    Restart=on-failure
    LimitNOFILE=65536

    [Install]
    WantedBy=multi-user.target
    ```
3. vi gitlab-runsvdir.service
    ```yaml
	[Unit]
	Description=GitLab Runit supervision process
	After=multi-user.target
	
	[Service]
	ExecStart=/opt/gitlab/embedded/bin/runsvdir-start
	Restart=always
	
	[Install]
	WantedBy=multi-user.target
    ```
    
    ```json
    name: etcd-1
    data-dir: /opt/etcd-v3.2.6/data
    listen-client-urls: http://0.0.0.0:2379,http://0.0.0.0:2379
    advertise-client-urls: http://0.0.0.0:2379,http://0.0.0.0:2379
    listen-peer-urls: http://0.0.0.0:2380
    initial-advertise-peer-urls: http://0.0.0.0:2380
    initial-cluster: etcd-1=http://0.0.0.0:2380
    initial-cluster-token: etcd-cluster-token
    initial-cluster-state: new
    ```
4. vi frp.service
    ```yaml
    [Unit]
	Description=frp server
	After=network.target
	[Service]
	Type=simple
	ExecStart=/usr/local/frp/frps -c /usr/local/frp/frps.ini
	Restart=always
	[Install]
	WantedBy=multi-user.target
    ```
    
    ```ini
    [common]
    bind_port = 9030

    [ssh]
    bind_addr=0.0.0.0
    listen_port = 9029
    ```
5. vi grafana.service
    ```yaml
    [Unit]
	Description=grafana
	After=network.target
	[Service]
	Type=simple
	LimitNOFILE=8192
	WorkingDirectory=/opt/grafana
	ExecStart=/opt/grafana/bin/grafana-server -config=/opt/grafana/conf/custom.ini
	Restart=always
	[Install]
	WantedBy=multi-user.target
    ```
6. vi prometheus.service
    ```yaml
    [Unit]
	Description=prometheus
	After=network.target
	[Service]
	Type=simple
	LimitNOFILE=8192
	WorkingDirectory=/opt/prometheus/
	ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml --web.listen-address=0.0.0.0:9020
	Restart=always
	[Install]
	WantedBy=multi-user.target
    ```
    
###### tags: `Linux` `systemd`