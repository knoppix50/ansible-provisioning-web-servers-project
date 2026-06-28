# Provisioning Web Servers with Ansible.

## Getting Started

Instructions to set up and run the Ansible deployment environment on AWS EC2 instances

### Dependencies

```
Control Node: Linux/Unix with Ansible core 2.15+ and Python 3.9+ installed.
Managed Nodes: 3 AWS EC2 instances running RHEL/CentOS-based Linux.
Network: SSH access (Port 22) enabled from Control Node to Managed Nodes via public key authentication.
```

### Installation

Step by step explanation of how to get a dev environment running.

List out the steps

```
1. Configure Inventory: Add target node internal hostnames to the inventory.ini file under the [aws] group.
2. Define Variables: Specify ansible_user, ansible_ssh_private_key_file, and ansible_python_interpreter in the inventory vars section.
3. Silence Warnings: Create an ansible.cfg file with interpreter_python = auto_silent to clear terminal logs.
4. Deploy Playbook: Execute the automation script from the master node terminal.

bash
ansible-playbook -i inventory.ini playbook.yml

```

## Testing

Verification steps to validate the infrastructure deployment

### Break Down Tests

Explain what each test does and why

```
Connectivity Test: Verifies active SSH communication across the nodes.

ansible aws -i inventory.ini -m ping

Firewall Rules Verification: Confirms ports 80 and 443 are permanently allowed.

ansible aws -i inventory.ini -m shell -a "firewall-cmd --list-ports" --become

Service Status Verification: Validates that Nginx is running and enabled on boot.

ansible aws -i inventory.ini -m shell -a "systemctl status nginx" --become

HTTP Redirection Test: Verifies local 301 redirection responses from the web server.

ansible aws -i inventory.ini -m shell -a "curl -I http://localhost" --become
```

## Project Instructions

- Automated security baseline deployment via firewalld package configuration.
- Directory structure validation using block, fail, and rescue error handling.
- Modular web architecture design utilizing a reusable webserver role.
- Iterative site provisioning using Ansible loops for explicit permission mapping (mode: '0770').
- Dynamic configuration engine leveraging Jinja2 templating (nginx.conf.j2) linked with automated service notification handlers.

## Built With

Ansible: Infrastructure as code orchestration engine.
Nginx: Lightweight HTTP proxy and web server engine.
Firewalld: Dynamic firewall manager for Linux environments.
AWS EC2: Cloud computing platform hosting master and worker instances.


## License

[License](LICENSE.txt)
