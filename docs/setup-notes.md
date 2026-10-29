# Homelab Setup Notes

These are some notes about how I set up my Linux homelab and the problems I ran into along the way.

## 1. Virtual Machines

I created two Ubuntu Server virtual machines using VirtualBox:

- **Homelab** (`192.168.56.10`) — runs my bachelor's application using Docker.
- **Monitoring** (`192.168.56.20`) — runs Prometheus and Grafana.

Both VMs have two network adapters. NAT is used for internet access, while Host-Only networking allows the VMs and my Windows PC to communicate.

I configured static IP addresses using Netplan.

## 2. SSH and Firewall

I enabled SSH so I could manage both servers remotely.

I also configured UFW on both VMs. On the Homelab server, port 9100 is accessible from the Monitoring VM so Prometheus can collect Node Exporter metrics.

On the Monitoring VM, Grafana's port 3000 is accessible from my Windows PC.

The firewall configuration is described in [ufw-rules.md](../configs/ufw-rules.md).

## 3. Application Deployment

I installed Docker and Docker Compose on the Homelab server.

I then deployed my bachelor's project, an employee scheduling application, using Docker Compose.

The application consists of three containers:

- **Frontend:** React application served by Nginx.
- **Backend:** Java Spring Boot application.
- **Database:** PostgreSQL.

I tested the deployment by opening the application from my Windows PC and logging in.

## 4. Monitoring

I installed Node Exporter on the Homelab server to provide system metrics.

On the Monitoring VM, I installed Prometheus and configured it to collect metrics from `192.168.56.10:9100` every 15 seconds.

I then installed Grafana, connected it to Prometheus, and imported the Node Exporter Full dashboard to monitor CPU, memory, disk, and network usage.

## 5. Troubleshooting

During deployment, I encountered CORS and JWT authentication issues. I investigated the backend logs, adjusted the configuration, and rebuilt the application.

I also encountered CPU soft-lockup warnings while running the virtual machines. I checked the VirtualBox logs and found that it was using the Windows hypervisor through NEM. This might be related to the performance problems, but I haven't confirmed the cause.

I left the hypervisor configuration unchanged because I also use Docker Desktop on Windows.

## 6. What I Learned

This project helped me get more comfortable working with Linux servers, configuring networks, using SSH, managing Docker containers, and setting up monitoring.

It also gave me more experience troubleshooting problems by checking logs and testing configuration changes.