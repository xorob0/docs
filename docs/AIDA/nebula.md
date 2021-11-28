# Installing on raspberry pi
```sh
mkdir /opt/nebula
cd /opt/nebula
wget https://github.com/slackhq/nebula/releases/download/v1.5.0/nebula-linux-arm64.tar.gz
sudo mkdir /opt/nebula
sudo tar -C /opt/nebula -xvf nebula-linux-arm64.tar.gz
rm -Rf /opt/nebula/nebula-linux-arm64.tar.gz
cd /opt/nebula
```