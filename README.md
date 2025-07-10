# Azure Load Balancer + App Gateway + VMSS Lab
🔧 by ifeOps

This is a hands-on networking lab project showcasing how to set up a scalable and resilient Azure architecture using:

- Azure Load Balancer (L4, TCP)
- Azure Application Gateway (L7, HTTP)
- Virtual Machine Scale Set (VMSS)
- NGINX on Linux VMs
- Custom health probes
- Network troubleshooting (502 errors)
- Azure Bastion
- Azure Monitor, NSGs, and Network Watcher

---

## 🧱 Architecture

![Architecture Diagram](architecture-diagram.png)

### 🏗️ Components:
- **VM Scale Set** running Ubuntu + NGINX
- **Standard Load Balancer** distributing TCP traffic on port 80
- **Application Gateway v2** with custom health probe
- **Azure Bastion** for secure VM access
- **NSG rules** allowing HTTP traffic

---

## 🚀 Project Goals

- Learn real-world VMSS and Layer 4/7 routing
- Fix a 502 Gateway error by applying custom probes and upgrading instances
- Understand how Azure networking components integrate
- Document setup for reuse, hiring, and public reference

---

## 🛠️ Steps Summary

1. Deploy Ubuntu-based VMSS
2. Install and configure NGINX (script provided)
3. Create Standard Load Balancer and connect to VMSS
4. Create Application Gateway
5. Add backend pool using VMSS
6. Create custom HTTP probe (`/`, port 80)
7. Attach probe to HTTP setting
8. Upgrade VMSS instances to apply changes
9. Test Load Balancer and App Gateway IPs
10. Enable Diagnostics & Azure Monitor

---

## 🧪 Troubleshooting Learned

- 💡 `502 Bad Gateway` on App Gateway? Check backend health + upgrade VMSS
- 💡 NSG rules must allow inbound TCP 80
- 💡 Health probe must match port and path
- 💡 App Gateway does NOT auto-apply config to VMSS — upgrade needed every time

#####  See screenshots folder for proof of successful deployment and error resolution.
---

## 🖥️ NGINX Setup Script (Ubuntu)

```bash
#!/bin/bash
sudo apt update -y
sudo apt install nginx -y
echo "<h1>Welcome from $(hostname)</h1>" | sudo tee /var/www/html/index.nginx-debian.html
sudo systemctl restart nginx

