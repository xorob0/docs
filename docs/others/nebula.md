# Nebula

## Install on ubuntu
```sh
mkdir /opt/nebula
cd /opt/nebula
wget https://github.com/slackhq/nebula/releases/download/v1.2.0/nebula-linux-amd64.tar.gz
sudo mkdir /opt/nebula
sudo tar -C /opt/nebula -xvf nebula-linux-amd64.tar.gz
sudo ufw allow 4242/udp
cd /opt/nebula
chmod +x nebula-cert
./nebula-cert ca -name "Managment network"
wget https://raw.githubusercontent.com/slackhq/nebula/master/examples/config.yml
```

Source:
https://blog.galt.me/nebula-mesh-vpn-on-ubuntu/

## Create a certificate

```
./nebula-cert sign -name "nimbus" -ip "10.200.0.1/24"

./nebula-cert sign -name "macbook" -ip "10.200.0.2/24" -groups "laptop,home,ssh"
./nebula-cert sign -name "iphone" -ip "10.200.0.3/24" -groups "mobile,home,ssh"
./nebula-cert sign -name "celty" -ip "10.200.0.4/24" -groups "server,home,ssh"
./nebula-cert sign -name "aida" -ip "10.200.0.5/24" -groups "server,home,ssh"
```

edit `config.yml`

## Setups
### Linux
Install with:
```bash
mkdir /opt/nebula
cd /opt/nebula
wget https://github.com/slackhq/nebula/releases/download/v1.2.0/nebula-linux-amd64.tar.gz
sudo mkdir /opt/nebula
sudo tar -C /opt/nebula -xvf nebula-linux-amd64.tar.gz
sudo ufw allow 4242/udp
```
nebula.sh
```bash
#!/bin/bash

/opt/nebula/nebula -config /opt/nebula/config.yml
```
/etc/systemd/system/nebula-start.service
```bash
[Unit]  
Description=Start Nebula Mesh VPN as a service.  
[Service]  
Type=simple  
ExecStart=/bin/bash /home/root/nebula-start.sh  
[Install]  
WantedBy=multi-user.target
```
```
sudo chmod 644 /etc/systemd/system/nebula-start.service
sudo systemctl daemon-reload
sudo systemctl enable nebula-start.service
sudo systemctl start nebula-start.service
sudo systemctl status nebula-start.service
```
### MacOS
Put your `crt` and `key` files in `/opt/nebula`

/Library/LaunchAgents/nebula.plist
```plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.nebula.startup</string>

    <key>OnDemand</key>
    <false/>

    <key>LaunchOnlyOnce</key>
    <true/>

    <key>UserName</key>
    <string>xorob0</string>

    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/nebula</string>
        <string>-config</string>
        <string>/opt/config.yml</string>
    </array>
</dict>
</plist>
```
