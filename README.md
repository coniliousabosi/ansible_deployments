# ansible_deployments
Ansible playbook playbooks for Linux , Splunk and observe deployments 
# Observe Agent Installation on RHEL Servers

This repository contains an Ansible playbook to install, configure, enable, and validate the Observe Agent on Red Hat Enterprise Linux (RHEL) servers.

The playbook adds the Observe Gemfury YUM repository, installs the `observe-agent` package, initializes the agent configuration, enables host monitoring, enables log collection, and verifies the agent status after installation.

---

## Purpose

This playbook automates the deployment of the Observe Agent across multiple RHEL servers using Ansible.

It enables collection of:

* Host metrics
* Host logs
* RED metrics
* Agent self-monitoring data
* Fleet monitoring information

---

## Requirements

Before running this playbook, ensure you have:

* Ansible installed on the control node
* SSH connectivity to target RHEL servers
* Sudo/root privileges on target systems
* A valid Observe ingest token
* The correct Observe collection URL

---

## Variables

Update the following variables before execution:

```yaml
observe_token: "Replace_was"
observe_url: "https://00000.collect.observeinc.com/"
```

Replace:

* `observe_token` with your Observe ingest token
* `observe_url` with your Observe collection endpoint

---

## Playbook Workflow

The playbook performs the following operations:

1. Adds the Observe Gemfury YUM repository
2. Installs the Observe Agent package
3. Initializes the Observe Agent configuration
4. Enables host monitoring
5. Enables host log collection
6. Enables self-monitoring and fleet monitoring
7. Restarts and enables the Observe Agent service
8. Validates the Observe Agent status
9. Displays the agent status output

---

## Usage

Run the playbook using:

```bash
ansible-playbook -i inventory install_observe_agent.yml
```

Example inventory:

```ini
[rhel_servers]
server1 ansible_host=192.168.1.10
server2 ansible_host=192.168.1.11
```

---

## Security Best Practices

Do not hardcode sensitive tokens in production environments.

Recommended alternatives:

* Ansible Vault
* Environment variables
* External secrets management solutions

Example using Ansible Vault:

```bash
ansible-vault encrypt vars.yml
```

---

## Verify Installation

Check Observe Agent status:

```bash
observe-agent status
```

Check systemd service:

```bash
systemctl status observe-agent
```

---

## Notes

The playbook installs the Observe Agent exclusively from the Observe Gemfury repository by disabling all other repositories during installation.

```yaml
disablerepo: "*"
enablerepo: "fury"
```

This helps ensure package consistency and controlled installation sources.

---

## Technologies Used

* Ansible
* RHEL / Linux
* OpenTelemetry concepts
* Observe Agent
* Systemd
* YUM Package Management

---

## Author

Conilious Abosi

Senior Security Engineer | Splunk Consultant | Observability & Cloud Enthusiast

