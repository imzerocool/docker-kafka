# /etc/systemd/system/kafka.service
[Unit]
Description=FT-cloud KAFKA Service
After=docker.service
Requires=docker.service

[Service]
TimeoutStartSec=0
Restart=always
ExecStartPre=-/usr/bin/docker stop kafka_zk
ExecStartPre=-/usr/bin/docker rm -v kafka_zk
ExecStart=/usr/bin/docker run --name kafka_zk -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=10.2.2.200 --env ADVERTISED_PORT=9092  image:latest
ExecStop=/usr/bin/docker stop kafka_zk

[Install]
WantedBy=multi-user.target
