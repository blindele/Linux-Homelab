# UFW Firewall Rules

I used UFW to control which connections are allowed between the two Ubuntu servers.

## Homelab VM (192.168.56.10)

- SSH (port 22) — remote server access.
- TCP port 9100 — allows the Monitoring VM (192.168.56.20) to collect Node Exporter metrics.

Port 9100 is restricted to the Monitoring VM instead of being open to the entire network.

## Monitoring VM (192.168.56.20)

- SSH (port 22) — remote server access.
- TCP port 3000 — allows the Windows host (192.168.56.1) to access Grafana.

Grafana access is restricted to the Windows host.

Both servers have UFW enabled.