# Umami Deploy for CV Website

This repository contains a production-ready deployment of [Umami Analytics](https://umami.is/) for my CV website [ardoabel.eu](https://ardoabel.eu), running on a Google Cloud VM with Docker and Nginx reverse proxy.

---

## 🔧 Features
- **Umami Analytics**: privacy-friendly web analytics
- **Docker Compose**: one-command deployment
- **Nginx Reverse Proxy**: secure HTTPS access via Let's Encrypt
- **Environment Separation**: `.env` for secrets, `.env.example` for sharing config
- **GitHub Backup**: Infrastructure as Code – easy to redeploy or restore

---

## 🏗 Architecture

```mermaid
flowchart TD
    subgraph Internet
        B[Browser/Visitor]
    end

    subgraph GCP_VM[Google Cloud VM]
        direction TB
        N[Nginx Reverse Proxy<br/>stats.ardoabel.eu:443]
        U[Umami Container<br/>localhost:3000]
        D[Postgres DB Container]
    end

    B -->|HTTPS| N -->|Proxy| U
    U --> D


🚀 Deployment

1. Clone the repository
git clone git@github.com:Xloaded/umami-deploy.git
cd umami-deploy

2. Copy environment file
cp .env.example .env
nano .env
#NB(Fill in the Postgres password and secrets.)

3. Start services
docker compose pull
docker compose up -d

4. Configure Nginx + SSL

Certificates are handled via Let’s Encrypt (certbot). Default Nginx config is in nginx/stats.ardoabel.eu.

⸻
📂 Repository structure
umami-deploy/
├── docker-compose.yml        # Docker services
├── .env.example              # Example environment variables
├── nginx/                    # Nginx reverse proxy configs
│   └── stats.ardoabel.eu
├── scripts/                  # Helper scripts
│   └── plausible-wait.sh
└── README.md                 # Documentation

🛡 Security Notes
	•	Do not commit .env files with real secrets.
	•	.gitignore excludes sensitive files.
