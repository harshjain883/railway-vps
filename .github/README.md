<div align="center">

# 🚀 Railway Ubuntu SSH Server

Lightweight, high-speed, and permanent Ubuntu environment hosted on Railway with direct SSH access via TCP Proxy.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/template)

</div>

---

## ✨ Features

* **Ubuntu Latest Base:** Fully updated system with basic development essentials.
* **Direct SSH Access:** Pre-configured OpenSSH server running inside Docker.
* **Persistent Networking:** Uses Railway Native TCP Proxy (no random port resets, no tunnel timeouts).
* **Pre-installed Packages:** Python3, Pip, Git, Wget, Curl, Nano, Sudo, and OpenSSH.
* **Automatic Log Output:** Automatically formats and displays full connection credentials in deployment logs.

---

## 📁 Repository Structure

```text
├── Dockerfile      # Core container build and SSH configuration
└── README.md       # Project documentation
