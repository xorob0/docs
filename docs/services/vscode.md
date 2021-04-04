# Visual Studio Code

## Compose

```
version: "3.3"
services:
  vscode:
    container_name: vscode
    image: codercom/code-server
    restart: unless-stopped
    volumes:
      - /configs:/configs
      - /configs/vscode:/home/coder/.config
      - /configs/vscode:/root/.config
```
