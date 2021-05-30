# Ombi

## Compose

```
version: '3.3'
services:
  ombi:
    image: ghcr.io/linuxserver/ombi:development
    container_name: ombi
    restart: unless-stopped
    volumes:
      - /configs/ombi-dev:/config
```

## Tips

### V3

I really adivise you to use the `development` tag to enjoy the new version.


### CSS

To disable the useless tabs I used:
```
#nav-adminDonate {
display: none
}
#nav-featureSuggestion {
display: none
}
```