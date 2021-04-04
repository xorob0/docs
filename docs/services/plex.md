# Plex

[Plex Media Server](https://www.plex.tv/) is a streaming service you can host at home (with your own content).

## Compose

```
version: '3.3'
services:
  plex:
    image: ghcr.io/linuxserver/plex
    container_name: plex
    restart: unless-stopped
    volumes:
      - /configs/plex:/config
      - /HDD1/Media/TV-Shows:/tv
      - /HDD1/Media/Movies:/movies
      - /HDD1/Media/Lives:/lives
    tmpfs:
      - /tmp
    devices:
      - /dev/dri:/dev/dri
```
I'm using [linuxserver.io's image](https://docs.linuxserver.io/images/docker-plex)

### tmpfs

Nothing really special on this docker-compose, except for the `tmpfs` line.

You can thing of `tmpfs` as a "mountpoint to RAM". Every files written to `/tmp` is written to RAM.

I am using this so my transcoded files don't have to be written to my SSD (because it would worn it out pretty fast) or my ZFS pool (which is slow in comparaison to RAM or my SSD).

### devices

To use QuickSync for transcoding I need to pass `/dev/dri` to the container. After that everything just works.

## Tips

### Put your thumnails on your SSD

I used to have my thumbnails and my preview images on my HDD, this makes the UI feels really slow. But on the other hand these images can take up a lot of space, I'm currently at 50Go for my Plex Media Server folder. This could be mitigated with a CDN but might get you bad performances on local network.

### Get Plex Pass

If you want to use Plex the way I am, get a Plex Pass! This will unlock some really nice features and also support the devs

### Disable Online Media Sources

One of the first things I did was disabling the free plex sources, I don't use them and find that they mostly clutter the UI.
![Online Media Sources](../assets/online_media_sources.png)
The only one I kept enabled is the Tidal one. I advise you to keep it enabled and add a free tidal account. This will add the soudtracks to your movies and TV shows.

### Remote access

Plex comes with integrated remote access management. It works well, but does not allow for a lot of optimisation. I decided to not use it.

![Remote Access disabled](../assets/remote_access.png)

Instead I set up a "Custom server access URL" under "Network"

![Custom server access URL](../assets/custom_access_url.png)

For this to work I am routing with Caddy #TODO: add link to caddy

This has several benefits:

- I don't get blocked by firewall when trying to listen to my music at the ofice
- I can use cloudflare's CDN for my images (they don't allow videos to be cached anymore)
- Every services available outside my network is managed by my reverse proxy, meaning I have more control about it.

You need to specify the port even if using some standard http/https ports.

### Don't use a CDN if you're going to use Plex locally

If you use a CDN evey stream will have to go through the CDN, this will give you pretty bad perfomances on local network even if it can improves performances remotely.

This could be circumvented with some DNS magic but I did not try it yet.

### Transcoder settings

If you want to use `tmpfs` as your transcoding folder, you should set it in the "Transcoder" settings:

![Transcoder settings](../assets/transcoder_path.png)

I advise you to use `/tmp` since I had some issues using other directories. It seems like the library used for EAC decoding was not using the path set up in the settings and would always go to `/tmp`.

If it is not enabled, you should enable:

- HDR tonemapping: This makes HDR content compatible with SDR devices. If disabled your HDR content will look washed out on SDR devices
- Use hardware acceleration when available: This will use your GPU instead of you CPU for transocding

### Enable agents

In the "Agents" settings you can add some agents that require API keys, they will make more content available like alternatives posters for your movies. They might also help with content matching.
