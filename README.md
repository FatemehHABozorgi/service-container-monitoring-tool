# Service & Container Monitoring Tool with Ansible

## Overview

This tool monitors systemd services and Docker containers for status changes, such as restarts, failures, or transitions between active and inactive states. Upon detecting changes, the tool sends consolidated SMS notifications using a configurable API. It is automated using Ansible to ensure a seamless setup process across multiple servers.

## Features

- Automatically monitors all systemd services and Docker containers on the server.

- Detects and reports status changes, including failures and restarts.

- Consolidates multiple alerts into a single SMS.

- Stores the previous state persistently to avoid duplicate notifications.

- Fully automated deployment using Ansible.

## Requirements

### Server Requirements

- Linux environment with:

  - Python 3.7+

  - Systemd for service management

  - Docker (if monitoring containers)

- Workstation Requirements (for running Ansible):

  - Ansible 2.9+

## Setup Instructions

1. Clone the Repository
```
git clone https://github.com/yourusername/service-container-monitoring-tool.git
cd service-container-monitoring-tool
```
2. Configure Variables

Define the required variables in a YAML file (e.g., vars/monitoring_vars.yml):
```
sms_api_url: "https://sms-api.example.com/monitoring/sms_alarm"
sms_api_user: "your_username"
sms_api_pass: "your_password"
service_user: "your_user"
service_group: "your_group"
```
3. Update Ansible Inventory

Ensure the target servers are listed in your Ansible inventory file, e.g., inventory:
```
[all]
server1 ansible_host=192.168.1.10 ansible_user=your_ssh_user
server2 ansible_host=192.168.1.11 ansible_user=your_ssh_user
```
4. Run the Ansible Playbook

Execute the playbook to deploy the monitoring tool:
```
ansible-playbook -i inventory playbooks/setup_monitoring.yml --extra-vars "@vars/monitoring_vars.yml"
```
5. Verify Deployment

After running the playbook, verify that the monitoring service is active:
```
sudo systemctl status monitoring.service
```

## Project Structure
```
service-container-monitoring-tool/
├── README.md
├── ansible/
│   ├── playbooks/
│   │   └── setup_monitoring.yml
│   ├── roles/
│   │   └── monitoring/
│   │       ├── tasks/
│   │       │   └── main.yml
│   │       ├── templates/
│   │       │   ├── monitoring_tool.py.j2
│   │       │   └── monitoring.service.j2
│   │       └── files/
│   │           └── requirements.txt
├── monitoring_states.json (ignored in `.gitignore`)
└── logs/
    └── monitoring.log
```

## Logs

Logs are stored in ```logs/monitoring.log```. You can view logs using:
```
tail -f logs/monitoring.log
```

## Contributing
Contributions are welcome! Please fork the repository and create a pull request with your changes.

## Author
Created by Fatemeh Haji Agha Bozorgi.
