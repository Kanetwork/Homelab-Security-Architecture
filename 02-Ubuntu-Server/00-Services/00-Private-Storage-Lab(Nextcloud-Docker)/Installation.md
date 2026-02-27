## <u><strong>Lab Notes: Private Storage Lab (Nextcloud/Docker)v1.0</strong></u>

## 🏗️ Phase 1: Host Preparation & Security
System Update: Refreshed package lists and upgraded existing software to ensure a secure baseline.
        
        sudo apt update && sudo apt upgrade -y
Docker Installation: Installed the Docker engine and Docker Compose to handle container orchestration.
     
        sudo apt install docker.io docker-compose -y
        sudo systemctl enable --now docker

Identity & Access Management (IAM): Added the local user to the docker group to implement the principle of least privilege (allowing Docker management without constant sudo usage).

        sudo usermod -aG docker $USER
        newgrp docker 

## 🛠️ Phase 2: Automated Maintenance Configuration
Unattended Upgrades: Configured the server to automatically pull security patches.

Scheduled Reboots: Set the system to reboot at 02:00 AM if a kernel patch requires it. This ensures the system never runs on a vulnerable kernel.

Persistence Strategy: Verified restart always flags were ready for the containers to ensure 99.9% availability after reboots.

## 🚀 Phase 3: Container Orchestration (The Stack)
Directory Structure: Created a dedicated space for Infrastructure as Code (IaC).

        mkdir ~/nextcloud && cd ~/nextcloud
Configuration (YAML): Authored the docker-compose.yml defining two services:

MariaDB: The database backend (isolated from the public network).

Nextcloud: The application frontend (mapped to host port 8080).

Deployment: Launched the stack in detached mode.

        docker-compose up -d

## 🔍 Phase 4: Troubleshooting & Problem Solving
Permission Error: Encountered Permission Denied when running Docker. Resolved by identifying that Linux sessions do not automatically update GID/UID changes; used newgrp as a workaround.

Database Handshake: Observed a slight delay in database initialization; identified the "Race Condition" and confirmed that Docker's restart policy successfully retried the connection until the DB was ready.

✅ Phase 5: Verification & Post-Install
Service Audit: Verified containers were running and healthy.

        docker ps

Web Initialization: Accessed the dashboard via http[:]//192[.]168[.]56[.]10:8080

Admin Hardening: Manually created a unique Admin user (avoiding the default "admin" name) and enabled Recommended Apps.

Data Validation: Navigated to /var/lib/docker/volumes/ to verify where Docker is physically storing the persistent data on the host disk.