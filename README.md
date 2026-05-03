# infra-support-automation
Ansible automation for support engineer workstation setup

# Infrastructure & Support Automation Lab

## Project Overview
This repository contains an Ansible-based automation solution designed to provision and configure a high-performance workstation for a Support Engineer in a Fintech/Trading environment.

The goal of this project is to demonstrate **Infrastructure as Code (IaC)** principles, ensuring a consistent, repeatable, and secure environment setup.

## Key Automation Blocks
* **System Hardening & Tooling:** Automated installation of diagnostic tools (`htop`, `net-tools`, `netcat-openbsd`, `curl`) and system-wide updates.
* **Network Security:** Automated deployment of OpenVPN client configurations with secured file permissions (`0600`).
* **Operational Efficiency:** Implementation of custom Bash aliases to accelerate log analysis and incident troubleshooting.
* **Containerization:** Orchestration of a Docker-based environment, including a pre-configured **PostgreSQL 15** instance for local database testing.
* **Monitoring Ready:** Automated installation of **Prometheus Node Exporter** binary to ensure the workstation is ready for metrics collection.

## Technical Skills Demonstrated
* **Idempotency:** All tasks are designed to be run multiple times without causing system inconsistencies.
* **Variable Management:** Centralized configuration using Ansible variables for easy updates of software versions.
* **Secret Management:** Sensitive values (e.g. database passwords) are externalized via Ansible variables and can be protected with `ansible-vault`.
* **Binary Management:** Experience with automated downloading (via `get_url`) and manual installation of system binaries.

## How to Run

1. Install Ansible and Docker (Ubuntu 22.04/24.04):

   sudo apt update && sudo apt install -y ansible docker.io

   ansible-galaxy collection install community.docker

2. Run the playbook:

   ansible-playbook -i inventory/hosts.ini playbook.yml --ask-become-pass -e "deploy_user=$USER" -e "postgres_password=YourSecurePassword" -e "vpn_server_address=vpn.yourcompany.com"
   > **Note:** In Codespaces, just press `Enter` when asked for password. If you see a reboot error, add `--skip-tags "patch,upgrade"` to the command.
   >  **Note for Codespaces:** If you see any `ignore_errors` warnings about reboot or Docker service — just ignore them. PostgreSQL and Node Exporter will still work. If PostgreSQL container fails to start automatically, run:
> ```bash
> docker run -d --name test_trading_db -e POSTGRES_PASSWORD=YourSecurePassword -e POSTGRES_USER=postgres -e POSTGRES_DB=trading_db postgres:15
> ```

4. After completion, log out and back in (or run: newgrp docker)

5. Verify everything works:

   docker exec test_trading_db pg_isready -U postgres
   curl http://localhost:9100/metrics | head -3
