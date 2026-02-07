## <u><strong>Project: Private Storage Lab (Nextcloud/Docker)v1.0</stong></u>

## 📌 Overview
Built a self-hosted "Private Cloud" storage solution on an Ubuntu Server environment. The goal was to replace third-party cloud providers with a secure, locally-owned alternative for family media and document storage.

## 🎯 Objectives
- Deploy a secure, containerized nextcloud instance with automated maintaenance.
- Understand IAM application.
- Understand Principle of least privilege.

## 🧰 Tools & Technologies
- YAML
- Linux
- Nextcloud (app)
- MariaDB (Database)
- Virtual Lab Environment

## 🚀 Usage

1. Within you web browser navigate to the assigned IP address: Port number in this case 192.168.56.10:8080

2. Login the YAML code should pick up the in intial credentials and enable you to create a account as admin.

3. From here navigate around where you can view the DASHBOARD presented, upload files, photos etc. 

4. You also serve as admin and manage other account, to control access within the application.

## 🧪 Lab Setup

|Role | Product |
| :--- | :---|
| Virtualisation software | Virtualbox |
| OS | Ubuntu 24.04 LTS (Server) |
| OS | Ubuntu 24.04.3 (Noble) (Admin/client) |

## 📊 Results
![Nextcloud photo server](./Screenshots/Photo_Cloud_Svr.png) 
*Nextcloud Photo Server*

## 📚 Lessons Learned
A major part of this lab was overcoming deployment hurdles. Below are the key technical challenges I encountered and how I resolved them:

1. Issue: Docker Permission Denied
The Error: **'docker.errors.DockerException: Error while fetching server API version: Permission denied'**

* The Cause: My user account was not part of the docker Unix group, meaning I lacked the necessary permissions to communicate with the Docker daemon socket.

* The Fix: * Used **'sudo usermod -aG docker $USER'** to modify user groups. Identified that Linux group changes require a fresh login session to initialize. Used newgrp docker to immediately reload the group context without a full reboot.

* Security Lesson: Learned about the Principle of Least Privilege and how Docker group membership is effectively root-equivalent access on a Linux system.

2. Issue: newgrp Password Prompt Logic
The Error: Being prompted for a password when running newgrp docker and having my user password rejected.

* The Cause: Discovered that newgrp looks for a specific group password rather than a user password. Since no group password was defined, the authentication loop failed.

* The Fix: Performed a full session logout/login to force the OS to pick up the updated GID (Group ID) from the **'/etc/group'** file.

3. Issue: Database Handshake Timing
The Error: Nextcloud showing a **'"Database Refused Connection"'** screen on first launch.

* The Cause: A "Race Condition." The Nextcloud application container started faster than the MariaDB database container could initialize its internal file structure.

* The Fix: Implemented the restart: always policy in the docker-compose.yml. This allowed the application to automatically retry the connection until the database was ready to receive traffic.

## 🔮 Future Improvements
[ ] Implement Nginx Proxy Manager for SSL/TLS (HTTPS) encryption.

[ ] Configure Fail2Ban to prevent brute-force attacks on the Nextcloud login.

[ ] Automate backups of the Docker volumes to an external physical drive.
