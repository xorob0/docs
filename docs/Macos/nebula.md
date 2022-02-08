## Install
```
brew install nebula
```
## config
```
pki:
  ca: /opt/nebula/ca.crt
  cert: /opt/nebula/macbook.crt
  key: /opt/nebula/macbook.key
static_host_map:
  "10.200.0.1": ["195.201.24.209:4242"]
lighthouse:
  am_lighthouse: false
  interval: 60
  hosts:
    - "10.200.0.1"
listen:
  host: 0.0.0.0
  port: 0
punchy:
  punch: true
tun:
  disabled: false
  dev: utun9
  drop_local_broadcast: false
  drop_multicast: false
  tx_queue: 500
  mtu: 1300
  routes:
  unsafe_routes:
logging:
  level: info
  format: text
firewall:
  conntrack:
    tcp_timeout: 12m
    udp_timeout: 3m
    default_timeout: 10m
    max_connections: 100000
  outbound:
    - port: any
      proto: any
      host: any
  inbound:
    - port: any
      proto: any
      host: any
```

## Autostart
Add `/Library/LaunchDaemons/com.nebula.plist`
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
      <key>Label</key>
      <string>/usr/local/bin/nebula</string>
      <key>LaunchOnlyOnce</key>
      <true/>
      <key>ProgramArguments</key>
      <array>
          <string>/usr/local/bin/nebula</string>
          <string>-config</string>
          <string>/opt/nebula/config.yml</string>
      </array>
      <key>RunAtLoad</key>
      <true/>
  </dict>
</plist>
```
