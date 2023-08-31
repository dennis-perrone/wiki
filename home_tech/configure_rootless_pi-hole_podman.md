# Configure rootless Pi-hole with Podman

## Preparation Steps

- Add the proper ports to the firewall.
- Create data directories where desired.
- Add `25-pihole.conf` to `/etc/sysctl.d/`.
- Within `25-pihole.conf`, add `net.ipv4.ip_unprivileged_port_start=53`
- Run `sudo sysctl -p /etc/sysctl.d/25-pihole.conf`
- Disable the DNS Stub listener: `sudo sed -r -i.orig 's/#?DNSStubListener=yes/DNSStubListener=no/g' /etc/systemd/resolved.conf`.
- Restart the `systemd-resolved` service.

## Deploy the compose file

- Write the following file into `/containers/pihole/compose.yml`

  ```yaml
  version: "3"

  # More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
  services:
    pihole:
      container_name: pihole
      image: pihole/pihole:latest
      ports:
        - "53:53/tcp"
        - "53:53/udp"
        - "67:67/udp"
        - "8080:80/tcp"
        - "8443:443/tcp"
      dns:
        - "127.0.0.1"
        - "8.8.8.8"
      hostname: pihole
      memory: 512M
      environment:
        TZ: 'America/New_York'
        FTLCONF_LOCAL_IPV4: '192.168.1.10'
        TEMPERATUREUNIT: 'f'
        # WEBPASSWORD: 'set a secure password here or it will be random'
      # Volumes store your data between container upgrades
      volumes:
        - './data/etc-pihole:/etc/pihole:Z'
        - './data/etc-dnsmasq.d:/etc/dnsmasq.d:Z'
      #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
      cap_add:
        - NET_ADMIN # Required if you are using Pi-hole as your DHCP server, else not needed
      restart: unless-stopped
  ```

- Execute `podman-compose up -d`

## Create Service

- Create service unit in `/etc/systemd/system/pi-hole.service`

  ```bash
  [Unit]
  Description=Pi-Hole Pdman Container
  After=firewalld.service
  
  [Service]
  ExecStart=/usr/bin/podman-compose up -d /home/dperrone/containers/pihole/compose.yml
  ExecStop=/usr/bin/podman stop -t 2 pihole
  ExecStopPost=/usr/bin/podman rm pihole
  
  [Install]
  WantedBy=multi-user.target
  ```
  
## Post-configuration tasks

- Go into the container, run `pihole -a` to configure the admin password.

## References

1. [GitHub Gist](https://gist.github.com/bcambl/2307e5f5a5d309a4885907426a4e9846)
2. [Ansible Podman Deployment](https://github.com/ikke-t/ansible-podman-examples/blob/master/run-container-pihole-podman.yml)
3. [Create Pi-hole Service](https://jreypo.io/2021/03/12/running-pihole-as-a-podman-container-in-fedora/)
