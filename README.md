
<div align="center">

# ☁️ CasaOS Nextcloud Homelab

### Your own cloud. Your own server. Your control.

A self-hosted personal cloud and server monitoring environment built with open-source technologies.

**Store files · Access them remotely · Monitor your server**

<br/>

![Project Status](https://img.shields.io/badge/Project-Work%20in%20Progress-orange?style=flat-square)
![Ubuntu](https://img.shields.io/badge/OS-Ubuntu%20Server-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![Docker](https://img.shields.io/badge/Containers-Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Nextcloud](https://img.shields.io/badge/Cloud-Nextcloud-0082C9?style=flat-square&logo=nextcloud&logoColor=white)
![Tailscale](https://img.shields.io/badge/Network-Tailscale-242424?style=flat-square&logo=tailscale&logoColor=white)
![Netdata](https://img.shields.io/badge/Monitoring-Netdata-00AB44?style=flat-square&logo=netdata&logoColor=white)

</div>

---

## 📌 Table of Contents

- [What Is This Project?](#-what-is-this-project)
- [Why Build a Homelab?](#-why-build-a-homelab)
- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [How the System Works](#-how-the-system-works)
- [Architecture](#-architecture)
- [Current Implementation](#-current-implementation)
- [Getting Started](#-getting-started)
- [Security](#-security)
- [Roadmap](#-roadmap)
- [Documentation](#-documentation)
- [Contributing](#-contributing)

---

## 💡 What Is This Project?

This project turns a personal computer into a **private server** that can store files, provide remote access, and display system performance information.

Instead of depending entirely on a third-party cloud storage service, a self-hosted setup lets you manage your own storage and services on hardware you control.

The server runs Ubuntu Server and uses CasaOS to manage applications. Nextcloud provides the cloud storage interface, Tailscale enables private remote connectivity, and Netdata helps visualize server performance.

> **Project goal:** Learn how to build, manage, secure, and maintain a practical personal cloud using open-source software.

## 🎯 Why Build a Homelab?

| Challenge | What this project provides |
|---|---|
| Need access to files from different devices | Nextcloud for file storage and access |
| Need remote connectivity | Tailscale private network |
| Want to manage applications easily | CasaOS web dashboard |
| Need visibility into server performance | Netdata monitoring |
| Want to learn real infrastructure skills | Linux, Docker, networking, and server administration |

A homelab is also a useful learning environment for understanding how real-world IT infrastructure works.

## ✨ Features

### ☁️ Personal Cloud Storage
Nextcloud provides a web interface for accessing and managing files on your server.

### 🔐 Private Remote Access
Tailscale connects authorized devices through a private network, allowing access without deliberately exposing the server's services to the public internet.

### 🔒 HTTPS Connectivity
Tailscale Serve provides an HTTPS endpoint for accessing Nextcloud within the private Tailscale network.

### 📊 Server Monitoring
Netdata displays metrics such as CPU usage, memory consumption, disk activity, network traffic, and process information.

### 🐳 Containerized Applications
Docker runs the application services in containers, helping separate services and manage their deployment.

### 🖥️ Web-Based Server Management
CasaOS provides a graphical dashboard for managing applications and viewing server information.

---

## 🧰 Technology Stack

| Technology | Role | Why It Is Used |
|---|---|---|
| Ubuntu Server | Operating system | Provides the Linux server environment |
| CasaOS | Management interface | Simplifies application and server management |
| Docker | Container platform | Runs applications in isolated containers |
| Nextcloud | Cloud application | Provides personal file storage and access |
| PostgreSQL | Database | Stores structured application data in this deployment |
| Redis | Supporting service | Provides caching and other configured application support |
| Tailscale | Private networking | Connects authorized devices securely |
| Tailscale Serve | HTTPS access | Proxies requests to Nextcloud over the private network |
| Netdata | Monitoring | Visualizes system and process metrics |

---

## ⚙️ How the System Works

The setup has three main parts:

**1. The server**

Ubuntu Server runs on the host computer. CasaOS provides the management interface, and Docker runs the application containers.

**2. File access**

Nextcloud stores and serves files. An authorized laptop or phone can connect locally or through the private Tailscale network.

**3. Monitoring**

Netdata collects and displays system metrics so the server's resource usage and activity can be inspected.

## 🏗️ Architecture

```text
             LAPTOP / PHONE / PC
                      |
           +----------+----------+
           |                     |
       Local LAN            Remote Access
                                 |
                             Tailscale
                                 |
                                 v
                      +--------------------+
                      |    UBUNTU SERVER   |
                      |                    |
                      |      CasaOS        |
                      |        |           |
                      |       Docker       |
                      |        |           |
                      |   +----+-----+      |
                      |   |          |      |
                      |   v          v      |
                      | Nextcloud  PostgreSQL|
                      |   |                 |
                      |   v                 |
                      | File Storage        |
                      |                    |
                      | Redis (support)    |
                      |                    |
                      | Netdata Monitoring |
                      +--------------------+
```

*Conceptual diagram: actual traffic paths depend on the network and service configuration. Netdata is a monitoring service, not a network gateway.*

---

## ✅ Current Implementation

The following items have been tested during development:

- [x] CasaOS dashboard is accessible.
- [x] Nextcloud is installed and operational.
- [x] Nextcloud login has been verified.
- [x] Remote HTTPS access through Tailscale Serve has been tested.
- [x] Netdata dashboard displays server metrics.

### ⚠️ Work Still in Progress

- [ ] Configure and verify monitoring notifications.
- [ ] Implement automated backups.
- [ ] Test a complete backup restoration.
- [ ] Configure Windows desktop synchronization.
- [ ] Configure automatic mobile photo backup.
- [ ] Review and harden all exposed services.
- [ ] Update the Netdata agent and verify the reported version warning is resolved.

---

## 🚀 Getting Started

This section is an overview, not a complete tested installation script. Follow the official documentation for the versions you install.

### Prerequisites

- A computer suitable for running Ubuntu Server.
- A stable network connection.
- Administrative access to the host.
- Enough storage for files, application data, and backups.
- A second trusted device for testing access.

### Step 1 — Install Ubuntu Server

Install a supported Ubuntu Server release, configure networking, and apply available security updates.

### Step 2 — Install CasaOS

Follow the official installation instructions:

https://casaos.io/

After installation, access the dashboard from a trusted device on the local network.

### Step 3 — Deploy Nextcloud

Install or configure Nextcloud through the existing CasaOS setup. Verify that its application and database services are running and that you can sign in.

### Step 4 — Configure Private Remote Access

Install and authenticate Tailscale on the server and your trusted client devices. Configure Tailscale Serve to provide HTTPS access to Nextcloud.

Official documentation:

https://tailscale.com/kb/

### Step 5 — Configure Monitoring

Deploy Netdata and verify that CPU, memory, disk, network, and process metrics are visible.

Official documentation:

https://learn.netdata.cloud/

### Step 6 — Plan Backups

Create a backup strategy that covers files, databases, and configuration. Store backups separately from the server and test restoration before relying on the setup for important data.

---

## 🔐 Security Considerations

Self-hosting means you are responsible for protecting your data and maintaining the server.

- **Private access:** Keep remote access restricted to authorized devices.
- **No unnecessary port forwarding:** Avoid exposing Nextcloud, CasaOS, Netdata, SSH, or database ports directly to the public internet.
- **Authentication:** Use strong, unique passwords and enable additional authentication protections where available.
- **Updates:** Keep Ubuntu, containers, and applications updated.
- **Backups:** Maintain independent backups and test recovery.
- **Secrets:** Never commit passwords, API keys, Tailscale authentication keys, private keys, session identifiers, or secret environment files.
- **Screenshots:** Redact private IP addresses, device identifiers, email addresses, and personal files before publishing.

HTTPS protects traffic in transit; it does not replace authentication, patching, access controls, or backups.

---

## 🗺️ Roadmap

### Phase 1 — Foundation
- [x] Deploy CasaOS
- [x] Run Nextcloud
- [x] Test private HTTPS access
- [x] Run Netdata monitoring

### Phase 2 — Reliability
- [ ] Configure automated backups
- [ ] Perform a recovery test
- [ ] Configure monitoring notifications
- [ ] Resolve outstanding monitoring warnings

### Phase 3 — Productivity
- [ ] Configure desktop synchronization
- [ ] Configure mobile photo backup
- [ ] Document maintenance procedures

### Phase 4 — Hardening
- [ ] Review firewall and service exposure
- [ ] Review access permissions
- [ ] Document update and recovery procedures

---

## 📚 Documentation

Detailed guides for this project will be maintained here:

| Document | Description |
|---|---|
| [Architecture](docs/architecture.md) | System components and network design |
| [Installation](docs/installation.md) | Installation and configuration guide |
| [Remote Access](docs/remote-access.md) | Tailscale and HTTPS setup |
| [Monitoring](docs/monitoring.md) | Metrics, warnings, and notifications |
| [Backups](docs/backups.md) | Backup and recovery strategy |

*Create and commit each document before relying on its link.*

## 🤝 Contributing

Ideas, corrections, and documentation improvements are welcome.

1. Fork the repository.
2. Create a branch for your change.
3. Commit your improvements.
4. Open a Pull Request describing the change.

## 📄 License

No license has been selected yet. Add a `LICENSE` file before describing this project as open-source software with a specific reuse license.

---

<div align="center">

### Built to learn. Designed to improve. Powered by open source.

**CasaOS · Nextcloud · Tailscale · Netdata**

</div>
