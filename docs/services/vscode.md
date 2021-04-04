# Visual Studio Code
[Visual Studio Code](https://github.com/cdr/code-server) is a IDE written in Javascript, that means it can run in a browser. That's exactly what this container does.

[Visual Studio Code](https://github.com/cdr/code-server) is awesome to edit configs with its build-in autocompletion and highlightings for various config structures.

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
