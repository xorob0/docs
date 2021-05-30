
#### Portainer Setup
As I do almost everything from portainer I just fire it up and do everything from the commandline.
```
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /configs/portainer:/data portainer/portainer-ce
```
If I ran the migration lines this part should not even be needed.



https://raw.githubusercontent.com/portainer/templates/master/templates-2.0.json