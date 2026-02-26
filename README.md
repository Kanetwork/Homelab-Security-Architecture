## 🏗️ <u><strong> Homelab-Security-Architechture </strong></u>

Documentation of virtual lab environments including Ubuntu servers, attack machines and network security implimentation.

## 📂 Repository Structure

## [00-Network-Diagrams](/00-Network-diagrams/)
This directory contains all visual representations of the homelab environment, including topologies, logical layouts, and architectural overviews. These diagrams provide a high‑level understanding of how systems, networks, and security controls interconnect across the environment. They serve as the primary reference for planning, troubleshooting, and documenting infrastructure changes.

![Current topography](/00-Network-Diagrams/00-Homelab-topography.png)*Current topography*

## [01-Machine-Builds](/01-Machine-builds/)
This directory documents the full lifecycle of each machine type within my homelab—server, and admin workstations. 

Each machine includes:

* Baseline Build — the clean, initial configuration.
* Current Build — the actively deployed, up‑to‑date configuration.
* Hardening — security controls such as SSH configuration, firewall rules, patching standards, and privilege models.
* Monitoring — logging, alerting, and metrics collection for operational visibility.

|      | [Hosting Server](/01-Machine-builds/00-Ubuntu-LTS/Current-Build/README.md) | [Admin workstation](/01-Machine-builds/01-Ubuntu-Admin-Workstation/Current-Build/README.md) 
| :-- |:-- | :-- |
| **Machine** | <!--Image--> | <!--Image--> 
|**OS** | Ubuntu 24.04.3 LTS | Ubuntu (Noble)
| **Kernal** | Linux 6.8.0-94-generic | <!--Kernal--> 
 

## [02-Services](/02-Services/)
This directory covers the major services deployed within the homelab, such as storage platforms, monitoring stacks, and other operational components.
Each service includes:

* Architecture — how the service fits into the wider environment.
* Deployment — installation and configuration steps.
* Hardening — security measures specific to the service.
* Alerting & Dashboards — visibility, metrics, and operational monitoring.
* Change Logs — a historical record of improvements, deployments, and security changes.

1. ### [Private Storage Lab](/02-Services/00-Private-Storage-Lab(Nextcloud-Docker)/)

    Built a self-hosted "Private Cloud" storage solution on an Ubuntu Server environment. The goal was to replace third-party cloud providers with a secure, locally-owned alternative for family media and document storage.

<!-- 2. ### Monitoring-Stack -->

## [03-Security-Control](/03-Security-Control/)
This directory defines the overarching security framework for the homelab. It includes threat models, audit processes, logging standards, firewall policies, access control models, patching standards, and monitoring requirements. These documents establish the governance layer of the environment—ensuring consistency, compliance, and a structured approach to security across all systems and services.

<!--1. ### Threat Modeling 

2. ### Security Audit

3. ### Logging Standards

4. ### Firewall Policy

5. ### Access Control Model 

6. ### Patch Management Standard

7. ### Monitoring Requirments -->