# infra-support-automation
Ansible automation for support engineer workstation setup 
# Infrastructure & Support Automation Lab

## Project Overview
This repository contains an Ansible-based automation solution designed to provision and configure a high-performance workstation for a Support Engineer in a Fintech/Trading environment. 

The goal of this project is to demonstrate **Infrastructure as Code (IaC)** principles, ensuring a consistent, repeatable, and secure environment setup.

## Key Automation Blocks
* **System Hardening & Tooling:** Automated installation of diagnostic tools (`htop`, `net-tools`, `telnet`, `curl`) and system-wide updates.
* **Network Security:** Automated deployment of OpenVPN client configurations with secured file permissions (`0600`).
* **Operational Efficiency:** Implementation of custom Bash aliases to accelerate log analysis and incident troubleshooting.
* **Containerization:** Orchestration of a Docker-based environment, including a pre-configured **PostgreSQL 15** instance for local database testing.
* **Monitoring Ready:** Automated installation of **Prometheus Node Exporter** binary to ensure the workstation is ready for metrics collection.

## Technical Skills Demonstrated
* **Idempotency:** All tasks are designed to be run multiple times without causing system inconsistencies.
* **Variable Management:** Centralized configuration using Ansible variables for easy updates of software versions.
* **Binary Management:** Experience with automated downloading, checksum verification (via `get_url`), and manual installation of system binaries.

## How to Run
1. Ensure Ansible is installed on your local machine.
2. Install the required Docker collection:
   ```bash
   ansible-galaxy collection install community.docker
