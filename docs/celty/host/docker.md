# Docker
## Installation

```
apt remove docker docker-engine docker.io containerd runc
apt update
apt install apt-transport-https ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update
apt install docker-ce docker-ce-cli containerd.io
systemctl start docker
systemctl enable docker
```

## Portainer Setup

As I do almost everything from portainer I just fire it up and do everything from the command line.

```
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /configs/portainer:/data portainer/portainer-ce
```

After that I generate portainer from portainer 
