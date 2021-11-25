# Nebula

## Install on ubuntu
```sh
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