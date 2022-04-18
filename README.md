# Homelab

## Pihole

- Install Docker: https://phoenixnap.com/kb/docker-on-raspberry-pi
- Install Docker Compose: https://jfrog.com/connect/post/install-docker-compose-on-raspberry-pi/
- Set Web Password : `export WEB_PASSWORD=<password>`
- Install Pihole: https://github.com/pi-hole/docker-pi-hole/#quick-start
```yaml
version: "3"

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    # For DHCP it is recommended to remove these ports and instead add: network_mode: "host"
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp" # Only required if you are using Pi-hole as your DHCP server
      - "80:80/tcp"
    environment:
      TZ: 'Europe/Paris'
      WEBPASSWORD: ${WEB_PASSWORD}
    # Volumes store your data between container upgrades
    volumes:
      - './etc-pihole:/etc/pihole'
      - './etc-dnsmasq.d:/etc/dnsmasq.d'    
    #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    cap_add:
      - NET_ADMIN # Required if you are using Pi-hole as your DHCP server, else not needed
    restart: unless-stopped
```
- Install whitelist: https://github.com/anudeepND/whitelist

TODO:
- Optional lists in the whitelist 
- https://github.com/jacklul/pihole-updatelists
- https://discourse.pi-hole.net/t/commonly-whitelisted-domains/212
- https://github.com/kboghdady/youTube_ads_4_pi-hole
- DHCP?
